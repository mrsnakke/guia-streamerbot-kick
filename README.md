# Guía de configuración: Streamer.bot + Kick + OBS + Speaker.bot + YouTube Music

[![Video en YouTube](https://img.youtube.com/vi/YOzUVz0EuMU/0.jpg)](https://youtu.be/YOzUVz0EuMU)



## Requisitos previos

Descarga los siguientes archivos:

- `Speaker.bot-x64-0.1.5.zip` https://speaker.bot/get-started/installation
- `Streamer.bot-x64-0.2.8.zip` https://streamer.bot/
- `Kick.bot-v1.0.0.0.zip` https://github.com/Sehelitar/Kick.bot/releases/tag/v1.0.0
- `YouTube-Music-3.9.0.exe` https://github.com/th-ch/youtube-music/releases
- `Downstream Keyer` https://obsproject.com/forum/resources/downstream-keyer.1254/

---

## 1. Preparar la carpeta principal

1. Crea una carpeta llamada `Streamerbot`.
2. Extrae el contenido de `Streamer.bot-x64-0.2.8.zip` en esa carpeta.
3. Dentro de `Streamerbot`, crea una subcarpeta llamada `speakerbot`.
4. Extrae `Speaker.bot-x64-0.1.5.zip` dentro de la subcarpeta `speakerbot`.

---

## 2. Inicializar archivos

1. Ejecuta `speaker.bot.exe` y `streamer.bot.exe` una vez y ciérralos para generar archivos necesarios.

---

## 3. Instalar KickBot

1. Copia los archivos de `Kick.bot-v1.0.0.0.zip` dentro de la carpeta `Streamerbot/dlls`.
2. Visita: [Kick Tool Gist](https://gist.github.com/mrsnakke/ac7cad47ede0b71447d5b6654de2b396)
3. Haz clic en `Raw`, selecciona todo (`Ctrl + A`), copia el contenido.
4. En Streamer.bot: `Actions > Import > Import String` → pega el contenido → `Import > OK > Save`.

---

## 4. Conectar Kick

1. En `Actions`, busca **KickBot** → clic derecho → `Test Trigger`.
   - Si no aparece ventana, desactiva el **modo "No molestar"** en Windows.
2. Conecta tu cuenta de Kick:
   - **Broadcast**: cuenta principal.
   - **Bot Account**: opcional (puede ser otra cuenta).
3. Cuando el ícono de `Pusher WebSocket` esté en verde, estás conectado.

---

## 5. Configurar Speaker.bot

1. Abre Speaker.bot → `Settings > WebSocket Server`
   - Marca `Auto Start` → clic en `Start Server`.
2. En Streamer.bot → `Integrations > speaker.bot`
   - Marca `Auto Connect` y `Auto Reconnect` → clic en `Connect` → `Save`.

---

## 6. Configurar Voz (TTS)

1. Speaker.bot → `Settings > Speech Engines` → `Add` → selecciona `SAPI5`.
   - Agrega voces desde los paquetes de idioma de Windows si es necesario.
2. Speaker.bot → `Settings > Voice Aliases`
   - Nombre: `Sabina`
   - Voz: selecciona la voz que quieras.
   - Prueba con `Test Speak` → clic en `Add` → `Save`.

---

## 7. Activar comandos en Streamer.bot

1. Pestaña `Commands`: clic derecho en cada comando → `Enabled` (no debe haber ninguno en rojo).
2. Puedes editar el comando `!sp` si quieres usar otro nombre.

---

## 8. Integrar OBS (Puntos de canal)

### Instalar el plugin Downstream Keyer

1. Instálalo desde su página oficial.
2. Abre OBS → `Panel > Downstream Keyer`
3. Crea una escena llamada `Puntos de Canal`.
4. En la ventana `DSK`, haz clic en `+` y agrega la escena.

### Conectar OBS a Streamer.bot

1. OBS → `Herramientas > Ajustes del Servidor WebSocket`
   - Habilita las 2 primeras opciones.
2. En Streamer.bot:
   - `Stream Apps > Add`
   - Nombre: OBS v5.x
   - Marca `Auto Connect`, `Reconnect`, y `Retry Interval: 5`
3. OBS → `Mostrar información de conexión`
4. Copia IP, puerto y contraseña en Streamer.bot.
5. Aplica cambios en OBS y acepta permisos.
6. En Streamer.bot → clic derecho sobre el host creado → `Connect`.
   - Si aparece `Connected 2/2`, está todo listo.

---

## 9. Crear y vincular recompensas (Canjes)

1. Duplica la acción `Plantilla Canjes` en `Actions` → renómbrala (ej: `Dore Dore`) → `Enabled`.
2. En Kick:
   - `Perfil > Panel de Creador > Canal > Comunidad > Puntos de canal`
   - Crea una recompensa llamada `Dore Dore` (marca **Cerrar lista de pedidos**).
3. Reinicia Streamer.bot.
4. En `Actions > Dore Dore > Triggers`:
   - Clic derecho → `【custom - kick - Rewards-】` → selecciona `【Kick/Reward】Dore Dore`.
5. En OBS:
   - En la escena `Puntos de Canal`, agrega una fuente multimedia llamada `Dore Dore`.
   - Configura:
     - **No** bucle
     - **Sí** reiniciar al activar
     - Oculta la fuente (icono del ojo).
6. En Streamer.bot → `Sub-Actions`:
   - Modifica los tres `OBS Source Visibility State`:
     - Conexión: `OBS v5.x`
     - Escena: `Puntos de Canal`
     - Fuente: `Dore Dore`

_Repite este proceso para cada nuevo canje._

---

## 10. Usar !sr (YouTube Music)

1. Ejecuta `YouTube-Music-3.9.0.exe`.
2. Ve a `Plugins > API Server (Beta)`:
   - Activa `Enabled`.
   - En `Authorization Strategy`, selecciona `No Authorization`.

---

## 11. Comandos disponibles

| Comando            | Función                                       |
|--------------------|-----------------------------------------------|
| `!sp`, `!tts`      | Leer el mensaje con voz (TTS)                 |
| `!sr`              | Reproducir canción (nombre o link de YouTube) |
| `!play`, `!pause`, `!stop` | Control de reproducción          |
| `!next`, `!skip`   | Siguiente canción                             |
| `!song`            | Mostrar canción actual en el chat de Kick     |

---

## Notas importantes

- Siempre deben estar abiertos:
  - `Speaker.bot`
  - `speakerbot` (carpeta interna)
  - `YouTube-Music-3.9.0.exe`

---

## Disclaimer y Créditos

> ⚠️ Esta guía utiliza el repositorio original de **[Kick.bot de Sehelitar](https://github.com/Sehelitar/Kick.bot/releases/tag/v1.0.0)** como base para la conexión entre Streamer.bot y Kick.  
>  
> Además, el sistema de **[Song Request System v1.2 para YouTube Music](https://extensions.streamer.bot/t/song-request-system-v1-2-youtube-music/2743)** fue adaptado y reconstruido para funcionar correctamente con Kick en esta integración.

---

Guía creada y adaptada por MrSnakeVT
