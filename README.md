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

Este proyecto incluye **[Playit.gg](https://playit.gg)** integrado directamente en Docker Compose. Esto permite que tus amigos se conecten desde cualquier parte del mundo **sin necesidad de abrir puertos en tu router/módem**.

### Configuración inicial (solo la primera vez)

1. Ve a [playit.gg/account/setup](https://playit.gg/account/setup/wizard/new-account) y crea una cuenta gratuita.
2. Selecciona **Docker** como tu entorno.
3. La página te dará un `SECRET_KEY`. Copia esa clave.
4. Crea un archivo `.env` en la raíz del proyecto (al lado del `docker-compose.yml`) con el siguiente contenido:
   ```env
   PLAYIT_SECRET_KEY=TU_CLAVE_AQUI
   ```
5. Inicia todo con:
   ```bash
   docker compose up -d
   ```
6. Verifica que el agente esté conectado:
   ```bash
   docker logs playit-tunnel
   ```
   Deberías ver: `playit connected; tunnels loaded`.

7. Ve a [playit.gg/account/tunnels](https://playit.gg/account/tunnels) y crea **dos túneles**:

   | Túnel | Tipo | Puerto Local | Protocolo |
   |-------|------|--------------|-----------|
   | Java | Minecraft Java | `25565` | TCP |
   | Bedrock | Minecraft Bedrock | `19132` | UDP |

8. Playit te asignará una dirección pública (ejemplo: `tu-servidor.auto.playit.gg`).

> **Nota:** El archivo `.env` contiene tu clave secreta y está excluido del repositorio gracias al `.gitignore`. Nunca se subirá a GitHub.

## 🌐 Cómo Conectarse

### ☕ Jugadores de Java Edition
1. Abre Minecraft Java Edition.
2. Ve a **Multijugador** → **Añadir servidor**.
3. En **Dirección del servidor** ingresa:
   - **Misma computadora:** `localhost`
   - **Misma red Wi-Fi/LAN:** `IP_LOCAL` del host (ejemplo: `192.168.1.15`)
   - **Desde Internet (con Playit.gg):** `tu-servidor.auto.playit.gg`
4. Haz clic en **Listo** y luego conéctate.

*Puerto por defecto: `25565` (no es necesario especificarlo).*

### 📱 Jugadores de Bedrock Edition (Móviles, Consolas, Windows 10/11)
1. Abre Minecraft Bedrock Edition.
2. Ve a **Jugar** → pestaña **Servidores** → baja hasta el final → **Añadir servidor**.
3. Llena los campos:
   - **Nombre del servidor:** (Cualquier nombre, ejemplo: `Mi Server`)
   - **Dirección del servidor:**
     - **Misma red local:** `IP_LOCAL` del host
     - **Desde Internet (con Playit.gg):** `tu-servidor.auto.playit.gg`
   - **Puerto:** `19132` (o el que te haya asignado Playit)
4. Guarda y conéctate.

