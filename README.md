# Emby en Docker | Servidor multimedia personal

**Emby** es una potente plataforma para organizar y transmitir tu colección multimedia (películas, series, música, fotos) a cualquier dispositivo, con interfaz web moderna y soporte para DLNA.

📦 **Servicios incluidos**
- Emby Server (interfaz web y transcodificación)
- Volúmenes para configuración y librerías multimedia

---

⚙️ **docker-compose.yml**
```yaml
services:
  emby:
    image: lscr.io/linuxserver/emby:latest
    container_name: emby
    restart: unless-stopped
    network_mode: bridge
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Madrid
    volumes:
      - ./config:/config
      - ./movies:/data/movies
      - ./tv:/data/tv
      - ./music:/data/music
    ports:
      - "8096:8096"    # Acceso HTTP
      - "8920:8920"    # Acceso HTTPS (opcional)
```

---

▶️ **Instrucciones de uso**

1. **Preparar carpetas**
   ```bash
   mkdir -p emby/config emby/movies emby/tv emby/music
   ```

2. **Levantar el servicio**
   ```bash
   docker compose up -d
   ```

3. **Acceder a Emby**
   Abre tu navegador y visita:  
   👉 `http://localhost:8096`  
   (O `http://IP_DEL_SERVIDOR:8096` desde tu red)

4. **Configuración inicial**
   - Crea tu usuario administrador  
   - Añade carpetas multimedia (`/data/movies`, `/data/tv`, `/data/music`)  
   - Configura idioma y metadatos  

---

🧹 **Comandos útiles**
- Ver logs:
  ```bash
  docker logs -f emby
  ```
- Reiniciar contenedor:
  ```bash
  docker compose restart emby
  ```
- Detener y eliminar:
  ```bash
  docker compose down
  ```

---

🧱 **Volúmenes y persistencia**
Emby guarda su configuración en `./config` y tus medios en `./movies`, `./tv` y `./music`.  
Puedes hacer backup fácilmente copiando esas carpetas.

---

🖥️ **Recomendación adicional**
Puedes integrar Emby con **Traefik** o **Nginx Proxy Manager** para añadir HTTPS, dominios personalizados y autenticación segura.

