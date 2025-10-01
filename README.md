# 🌐 Meshtastic Broker + APRS Gateway + Telegram Bot (Docker)

Este proyecto proporciona un **stack completo** basado en Docker con tres servicios principales:

- 🔌 **Broker** → Conecta al nodo Meshtastic y expone una API JSONL.  
- 📡 **APRS Gateway** → Pasarela bidireccional entre Meshtastic y APRS (vía KISS TCP).  
- 🤖 **Telegram Bot** → Control remoto y consulta del estado de la red Meshtastic desde Telegram.  

👉 No se expone el código fuente. Todo se distribuye mediante **imágenes Docker** publicadas en **GitHub Container Registry (GHCR)**.

---

## 🚀 Requisitos

- [Docker](https://docs.docker.com/get-docker/)  
- [Docker Compose](https://docs.docker.com/compose/install/)  

---

## 📦 Instalación

1. Clonar este repositorio:

```bash
git clone https://github.com/jmmpcc/meshtastic-aprs-public.git
cd meshtastic-aprs-public
```

2. Copiar el archivo de variables de entorno y editarlo con tus datos:

```bash
cp .env-example .env
```

3. Levantar los servicios:

```bash
docker compose up -d
```

---

## ⚙️ Variables de entorno

El archivo `.env` controla los parámetros de configuración.  
Ejemplo (`.env-example`):

```dotenv
# === Nodo Meshtastic ===
MESHTASTIC_HOST=192.168.1.201
BROKER_PORT=8765
BACKLOG_PORT=8766

# === Telegram Bot ===
TELEGRAM_TOKEN=xxxxxxxxxxxxx
ADMIN_IDS=123456789

# === APRS Gateway ===
APRS_CALL=EB2XXX-11
KISS_HOST=host.docker.internal
KISS_PORT=8100
MESHTASTIC_CH=0
BOT_START_DELAY=90
```

---

## 🛠️ Servicios

### 🔌 Broker
- Imagen: `ghcr.io/jmmpcc/meshtastic-broker:latest`  
- Función: conecta al nodo Meshtastic y expone la API JSONL.  
- Puertos:
  - `8765` → Broker JSONL
  - `8766` → Backlog server (control interno)

### 📡 APRS Gateway
- Imagen: `ghcr.io/jmmpcc/meshtastic-aprs:latest`  
- Función: puente bidireccional entre Meshtastic y APRS (vía KISS TCP).  

### 🤖 Telegram Bot
- Imagen: `ghcr.io/jmmpcc/meshtastic-bot:latest`  
- Función: control remoto vía comandos de Telegram.  
- Necesita el token del bot (`TELEGRAM_TOKEN`) y los IDs de administradores (`ADMIN_IDS`).  

---

## 📥 Actualización

Para actualizar a la última versión publicada en GHCR:

```bash
docker compose pull
docker compose up -d
```

---

## 📝 Notas

- El código fuente **no está incluido** en este repo.  
- Todas las imágenes se publican automáticamente en **GitHub Container Registry (GHCR)** desde un repositorio privado.  
- Puedes inspeccionar y descargar las imágenes en:  
  👉 https://github.com/jmmpcc?tab=packages&repo_name=meshtastic-aprs-public  

---

## 📄 Licencia

Este proyecto está disponible bajo licencia **MIT**.  
