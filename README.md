# 🤖 Moody Bot - Asistente de Orientación Psicológica

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Telegram](https://img.shields.io/badge/Telegram-Bot-blue.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.15.0-orange.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

*Bot inteligente de Telegram que proporciona orientación psicológica básica mediante análisis de emociones por voz, cuestionarios personalizados y conversación con IA.*

[🚀 Instalación](#-instalación) • [📱 Uso](#-uso) • [🛠️ Características](#%EF%B8%8F-características) • [📁 Estructura](#-estructura-del-proyecto) • [🔧 Configuración](#-configuración)

</div>

---

## ✨ Características Principales

### 🎯 **Análisis Integral**
- **4 tipos de terapia**: Familiar, Pareja, Individual, Adolescentes
- **Cuestionarios personalizados**: 6 preguntas específicas por tipo de terapia
- **Análisis de emociones por voz**: Usando CNN y características de audio
- **Conversación con IA**: Integración con Ollama LLM para chat empático

### 📊 **Reportes Profesionales**
- **PDFs detallados**: Análisis completo con recomendaciones profesionales
- **Envío automático por email**: Reportes enviados a especialistas
- **Resúmenes de conversación**: Análisis completo de toda la interacción
- **Recomendaciones personalizadas**: Generadas por IA según el perfil emocional

### 🎤 **Tecnología de Vanguardia**
- **Detección de emociones**: 6 emociones (tristeza, felicidad, ira, ansiedad, calma, neutral)
- **Análisis de audio**: Características RMS, ZCR, centroide espectral, tempo
- **IA conversacional**: Respuestas contextuales y empáticas
- **Fallback inteligente**: Sistema alternativo cuando falla la CNN

---

## 🚀 Instalación

### 📋 Prerrequisitos

- **Python 3.8+**
- **Telegram Bot Token** ([Crear bot](https://t.me/botfather))
- **Ollama** (opcional, para IA conversacional)
- **Gmail App Password** (opcional, para envío de emails)

### ⚡ Instalación Rápida

```bash
# 1. Clonar el repositorio
git clone https://github.com/ErickEduardoEspinozaTipantiza/MoodyTelegram.git
cd MoodyTelegram

# 2. Instalar dependencias
pip install -r requirements.txt

# 3. Configurar variables de entorno
cp .env.example .env
# Editar .env con tus credenciales

# 4. Verificar modelos (solo la primera vez)
python fix_models.py

# 5. Ejecutar el bot
python main.py
```

### 🔧 Configuración Manual

1. **Crear archivo `.env`**:
```env
# Bot de Telegram
TELEGRAM_BOT_TOKEN=tu_token_aqui

# Ollama (opcional)
OLLAMA_API_URL=http://localhost:11434

# Email (opcional)
EMAIL_USER=tu_email@gmail.com
EMAIL_PASSWORD=tu_app_password
```

2. **Instalar Ollama** (opcional):
```bash
# Windows/Linux/Mac
curl -fsSL https://ollama.com/install.sh | sh
ollama pull llama2  # o tu modelo preferido
```

---

## 📱 Uso

### 🎯 **Flujo Principal**

1. **Inicio**: `/start` - Seleccionar tipo de terapia
2. **Cuestionario**: Responder 6 preguntas personalizadas
3. **Análisis de voz**: Grabar audio de 10 segundos
4. **Resultados**: Recibir PDF con análisis completo
5. **Chat**: Conversar con IA sobre el análisis
6. **Resumen**: `/resumen` - Generar análisis de toda la conversación

### 📋 **Comandos Disponibles**

| Comando | Descripción |
|---------|-------------|
| `/start` | Iniciar o reiniciar el bot |
| `/help` | Mostrar ayuda completa |
| `/resumen` | Generar resumen de conversación |

### 🎭 **Tipos de Terapia**

- **👨‍👩‍👧‍👦 Terapia Familiar**: Dinámicas familiares y comunicación
- **💑 Terapia de Pareja**: Relaciones y comunicación de pareja
- **👤 Terapia Individual**: Crecimiento personal y autoconocimiento
- **👩‍🎓 Terapia para Adolescentes**: Apoyo específico para jóvenes

---

## 🛠️ Arquitectura Técnica

### 🧠 **Análisis de Emociones**

```python
# Modelo principal: CNN + Características de audio
Emociones detectadas: [sad, happy, angry, anxious, calm, neutral]
Confianza: 0.0 - 1.0
Características: RMS, ZCR, Centroide Espectral, Tempo
```

### 🔄 **Sistema de Fallback**

1. **CNN Principal**: TensorFlow + modelos entrenados
2. **Análisis Alternativo**: Características de audio + heurísticas
3. **Modo Texto**: Solo cuestionario si falla análisis de voz

### 💾 **Almacenamiento**

- **Sesiones**: JSON temporal para datos de usuario
- **Modelos**: Archivos .pkl y .h5 en directorio `/models`
- **PDFs**: Generación temporal en `/temp`

---

## 📁 Estructura del Proyecto

```
MoodyTelegram/
├── 📄 main.py                 # Aplicación principal del bot
├── 🔧 fix_models.py           # Script de verificación de modelos
├── ⚙️ requirements.txt        # Dependencias Python
├── 📋 .env                    # Variables de entorno
├── 
├── 📂 config/                 # Configuraciones
│   ├── settings.py            # Configuración general
│   └── therapy_questions.py   # Preguntas por tipo de terapia
├── 
├── 📂 handlers/               # Manejadores de eventos
│   ├── start_handler.py       # Comandos /start y /help
│   ├── therapy_handler.py     # Selección de terapia
│   ├── voice_handler.py       # Análisis de voz
│   └── chat_handler.py        # Chat con IA y /resumen
├── 
├── 📂 services/               # Servicios principales
│   ├── emotion_analyzer.py    # Análisis de emociones (CNN + alternativo)
│   ├── pdf_generator.py       # Generación de reportes PDF
│   ├── email_service.py       # Envío de emails
│   └── ollama_client.py       # Cliente para Ollama LLM
├── 
├── 📂 models/                 # Modelos de ML
│   ├── modelo_cnn.h5          # Red neuronal principal
│   ├── scaler.pkl             # Normalizador de características
│   ├── pca.pkl                # Reductor de dimensionalidad
│   └── label_encoder.pkl      # Codificador de emociones
├── 
├── 📂 utils/                  # Utilidades
│   └── helpers.py             # Funciones auxiliares
├── 
├── 📂 data/                   # Datos temporales
│   └── user_sessions.json     # Sesiones de usuarios
└── 
└── 📂 temp/                   # Archivos temporales
    └── *.pdf                  # PDFs generados
```

---

## 🔧 Configuración Avanzada

### 🎛️ **Variables de Entorno**

```env
# Obligatorias
TELEGRAM_BOT_TOKEN=your_token_here

# Opcionales
OLLAMA_API_URL=http://localhost:11434
EMAIL_USER=your_email@gmail.com
EMAIL_PASSWORD=your_app_password

# Rutas (auto-configuradas)
MODELS_PATH=models/
DATA_PATH=data/
TEMP_PATH=temp/
```

### 🔍 **Configuración de Modelos**

```bash
# Verificar estado de modelos
python fix_models.py

# Resultado esperado:
✅ Modelo CNN compatible
✅ scaler.pkl está OK
✅ pca.pkl está OK
✅ label_encoder.pkl está OK
✅ Sistema de análisis funcionando
```

### 📊 **Configuración de Ollama**

```bash
# Instalar modelos recomendados
ollama pull llama2:7b       # Modelo general
ollama pull llama2:13b      # Modelo más potente
ollama pull mistral:7b      # Alternativa ligera

# Verificar instalación
curl http://localhost:11434/api/version
```

---

## 🚨 Solución de Problemas

### ❗ **Problemas Comunes**

| Problema | Solución |
|----------|----------|
| `invalid load key` | Ejecutar `python fix_models.py` |
| Ollama no responde | Verificar `ollama serve` |
| Email no se envía | Configurar App Password de Gmail |
| Audio no se procesa | Verificar permisos de micrófono |

### 🔧 **Comandos de Diagnóstico**

```bash
# Verificar configuración completa
python test_setup.py

# Probar solo modelos
python fix_models.py

# Verificar dependencias
pip check
```

### 📝 **Logs y Debug**

```python
# Activar logs detallados
import logging
logging.basicConfig(level=logging.DEBUG)
```

---

## 🎨 Personalización

### 🏷️ **Cambiar Nombre del Bot**

Buscar y reemplazar "Moody" en:
- `start_handler.py`
- `pdf_generator.py`
- `email_service.py`
- `main.py`

### 🎭 **Agregar Nuevas Emociones**

1. Modificar `config/settings.py`:
```python
EMOTIONS = {
    "sad": "Tristeza",
    "happy": "Felicidad", 
    "angry": "Ira",
    "anxious": "Ansiedad",
    "calm": "Calma",
    "neutral": "Neutral",
    "excited": "Emoción"  # Nueva emoción
}
```

2. Reentrenar modelos con nuevos datos

### 📋 **Personalizar Preguntas**

Editar `config/therapy_questions.py`:
```python
THERAPY_QUESTIONS = {
    "individual": [
        "Tu pregunta personalizada aquí...",
        # ... más preguntas
    ]
}
```

---

## 🤝 Contribución

### 📥 **Contribuir al Proyecto**

1. Fork el repositorio
2. Crear rama feature: `git checkout -b feature/nueva-funcionalidad`
3. Commit cambios: `git commit -m 'Agregar nueva funcionalidad'`
4. Push a la rama: `git push origin feature/nueva-funcionalidad`
5. Crear Pull Request

### 🐛 **Reportar Bugs**

- Usar [GitHub Issues](https://github.com/ErickEduardoEspinozaTipantiza/MoodyTelegram/issues)
- Incluir logs y pasos para reproducir
- Especificar versión de Python y OS

---

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles.

---

## 👨‍💻 Autor

**Erick Eduardo Espinoza Tipantiza**
- GitHub: [@ErickEduardoEspinozaTipantiza](https://github.com/ErickEduardoEspinozaTipantiza)
- Email: crisgeopro2003@gmail.com

---

## 🙏 Agradecimientos

- **Telegram Bot API** - Framework de bots
- **TensorFlow** - Modelos de ML
- **Ollama** - IA conversacional local
- **ReportLab** - Generación de PDFs
- **Librosa** - Análisis de audio

---

<div align="center">

**⚠️ Nota Importante**

Este bot brinda orientación básica y **NO reemplaza** la consulta con un profesional de la salud mental. Para situaciones de crisis, contacta servicios de emergencia locales.

---

**¿Te gusta el proyecto? ¡Dale una ⭐!**

</div>
