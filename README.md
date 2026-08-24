# Minecraft Cross-Play Server (Java & Bedrock)

Este proyecto contiene la configuración de Docker Compose para desplegar rápidamente un servidor de Minecraft (usando Paper) que permite la conexión de jugadores tanto de **Java Edition** como de **Bedrock Edition**.

Compatible con **Windows**, **macOS** y **Linux**.

## 🚀 Requisitos

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (disponible para Windows, macOS y Linux).
- [Playit.gg](https://playit.gg/download) (opcional, para compartir el servidor por Internet sin abrir puertos).

## 🛠️ Instalación y Uso

1. Clona este repositorio o descarga los archivos.
2. Abre una terminal en la carpeta del proyecto.
3. Ejecuta el siguiente comando para iniciar el servidor en segundo plano:
   ```bash
   docker compose up -d
   ```
4. El servidor descargará la versión requerida, instalará los plugins automáticamente y se iniciará.

### Comandos útiles

| Comando | Descripción |
|---------|-------------|
| `docker compose up -d` | Iniciar el servidor en segundo plano |
| `docker logs -f mc-crossplay` | Ver los logs del servidor en tiempo real |
| `docker compose down` | Detener el servidor |
| `docker compose restart` | Reiniciar el servidor |

**Nota sobre los datos:** Todos los archivos del servidor (mundos, configuraciones, plugins) se guardarán en la carpeta `data/`. Esta carpeta está excluida en el `.gitignore` para evitar que subas mundos pesados a GitHub accidentalmente.

## 🔌 Plugins Automatizados (Cross-Play)

¡Buena noticia! No necesitas descargar ni instalar nada manualmente. El archivo `docker-compose.yml` está configurado para **descargar e instalar automáticamente** los plugins esenciales cada vez que inicies el servidor. Los plugins incluidos son:

- **[GeyserMC](https://modrinth.com/plugin/geyser)**: Permite que clientes de Bedrock se unan a un servidor Java.
- **[Floodgate](https://modrinth.com/plugin/floodgate)**: Permite a los jugadores de Bedrock autenticarse sin necesidad de tener una cuenta de Microsoft/Java.
- **[ViaVersion](https://modrinth.com/plugin/viaversion)**: Permite a versiones más nuevas del cliente conectarse a tu servidor.
- **[ViaBackwards](https://modrinth.com/plugin/viabackwards)**: Permite a versiones más antiguas conectarse.

## 🌍 Compartir el Servidor por Internet (Sin abrir puertos)

Para que tus amigos se conecten desde cualquier parte del mundo **sin necesidad de abrir puertos en tu router/módem**, usa [Playit.gg](https://playit.gg):

1. Descarga Playit.gg desde [playit.gg/download](https://playit.gg/download) (disponible para **Windows** y **macOS**).
2. Crea una cuenta gratuita e inicia sesión.
3. Crea **dos túneles** dentro de Playit:

   | Túnel | IP Local | Puerto | Protocolo |
   |-------|----------|--------|-----------|
   | Java | `127.0.0.1` | `25565` | TCP |
   | Bedrock | `127.0.0.1` | `19132` | UDP |

4. Playit te asignará una dirección pública (ejemplo: `tu-servidor.auto.playit.gg`).
5. ¡Comparte esa dirección con tus amigos y listo!

## 🌐 Cómo Conectarse

### ☕ Jugadores de Java Edition
En el menú Multijugador → "Añadir servidor":
- **Misma computadora:** `localhost`
- **Misma red Wi-Fi/LAN:** `IP_LOCAL` del host (ejemplo: `192.168.1.15`)
- **Desde Internet (con Playit.gg):** `tu-servidor.auto.playit.gg`

*Puerto por defecto: `25565` (no es necesario especificarlo).*

### 📱 Jugadores de Bedrock Edition (Móviles, Consolas, Windows 10/11)
En la pestaña Servidores → "Añadir servidor":
- **Nombre del servidor:** (Cualquier nombre)
- **Dirección del servidor:**
  - **Misma red local:** `IP_LOCAL` del host
  - **Desde Internet (con Playit.gg):** `tu-servidor.auto.playit.gg`
- **Puerto:** `19132`
