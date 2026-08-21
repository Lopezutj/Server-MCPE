# Minecraft Cross-Play Server (Java & Bedrock)

Este proyecto contiene la configuración de Docker Compose para desplegar rápidamente un servidor de Minecraft (usando Paper) que permite la conexión de jugadores tanto de **Java Edition** como de **Bedrock Edition**.

## 🚀 Requisitos

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (o Docker Engine y Docker Compose).

## 🛠️ Instalación y Uso

1. Clona este repositorio o descarga los archivos.
2. Abre una terminal en la carpeta del proyecto.
3. Ejecuta el siguiente comando para iniciar el servidor en segundo plano:
   ```bash
   docker compose up -d
   ```
4. El servidor descargará la versión requerida y se iniciará.

 para ver logs 
```bash
   docker logs -f mc-crossplay
```
 para detener el servidor 
```bash
   docker compose down
```
 para reiniciar el servidor
```bash
   docker compose restart
```

**Nota sobre los datos:** Todos los archivos del servidor (mundos, configuraciones, plugins) se guardarán en la carpeta `data/`. Esta carpeta está excluida en el `.gitignore` para evitar que subas mundos pesados a GitHub accidentalmente.

## 🔌 Plugins Automatizados (Cross-Play)

¡Buena noticia! No necesitas descargar ni instalar nada manualmente. El archivo `docker-compose.yml` está configurado para **descargar e instalar automáticamente** los plugins esenciales cada vez que inicies el servidor. Los plugins incluidos son:

- **[GeyserMC](https://modrinth.com/plugin/geyser)**: Permite que clientes de Bedrock se unan a un servidor Java.
- **[Floodgate](https://modrinth.com/plugin/floodgate)**: Permite a los jugadores de Bedrock autenticarse sin necesidad de tener una cuenta de Microsoft/Java.
- **[ViaVersion](https://modrinth.com/plugin/viaversion)**: Permite a versiones más nuevas del cliente conectarse a tu servidor.
- **[ViaBackwards](https://modrinth.com/plugin/viabackwards)**: Permite a versiones más antiguas conectarse.

## 🌐 Cómo Conectarse

La forma de conectarse depende de desde dónde estén jugando tus amigos. A continuación se detallan los datos que deben ingresar en su juego:

### ☕ Jugadores de Java Edition
En el menú Multijugador, haz clic en "Añadir servidor" e ingresa la siguiente Dirección del servidor (IP):
- **Si juegas en la misma PC que aloja el servidor:** `localhost` o `127.0.0.1`
- **Si juegas desde otra PC en la misma red Wi-Fi/LAN:** `TU_IP_LOCAL` (ejemplo: `192.168.1.15`)
- **Si juegas desde otra casa (Internet):** `TU_IP_PUBLICA` (Debes tener los puertos abiertos en tu router o usar herramientas como Playit.gg/Ngrok).
*Nota: El puerto por defecto para Java es `25565`. No es necesario especificarlo a menos que lo cambies.*

### 📱 Jugadores de Bedrock Edition (Móviles, Consolas, Windows 10/11)
En la pestaña Servidores, baja hasta el final y elige "Añadir servidor". Ingresa los siguientes datos:
- **Nombre del servidor:** (Cualquier nombre)
- **Dirección del servidor (IP):** 
  - **Misma PC o red local:** La `IP_LOCAL` de la computadora que aloja el servidor.
  - **Desde otra casa (Internet):** Tu `IP_PUBLICA` (Requiere abrir el puerto UDP en el router).
- **Puerto:** `19132` (Este es el puerto que GeyserMC utiliza por defecto para recibir a los jugadores de Bedrock).
