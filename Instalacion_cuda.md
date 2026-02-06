# 🎭 Guía Completa de Instalación de FaceFusion en Windows 11 con CUDA

## 📋 Requisitos del Sistema

- **Sistema Operativo:** Windows 11 (64-bit)
- **Procesador:** Ryzen 5 serie 7000 o superior
- **GPU:** NVIDIA RTX 3050 6GB (o cualquier GPU NVIDIA compatible con CUDA)
- **RAM:** Mínimo 8GB (recomendado 16GB)
- **Espacio en Disco:** Mínimo 10GB libres
- **Internet:** Conexión estable para descargar dependencias (~3-4 GB)

---

## 🚀 Instalación Paso a Paso

### **PASO 1: Instalar Miniconda**

#### Opción A - Descarga Manual (Recomendado)
1. Ve a: https://www.anaconda.com/download
2. Busca la sección **Miniconda** (está más abajo en la página)
3. Descarga **Miniconda3 Windows 64-bit**
4. Ejecuta el instalador descargado

**Configuración importante durante la instalación:**
- ✅ Selecciona: **"Just Me"** (solo para tu usuario)
- ❌ **NO marques:** "Add Miniconda3 to PATH environment variable"
- ✅ **SÍ marca:** "Register Miniconda3 as my default Python 3.X"

#### Opción B - Desde Command Prompt (Avanzado)
```cmd
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe -o miniconda.exe
start /wait "" miniconda.exe /InstallationType=JustMe /RegisterPython=0 /S /D=%UserProfile%\miniconda3
del miniconda.exe
```

---

### **PASO 2: Verificar Instalación de Miniconda**

1. Presiona **Windows + S** y busca: **"Anaconda Prompt (miniconda3)"**
2. Ábrelo y ejecuta:
```cmd
conda --version
```
3. Deberías ver algo como: `conda 25.11.1`

---

### **PASO 3: Crear Entorno Virtual para FaceFusion**

En **Anaconda Prompt**, ejecuta:

```cmd
conda create --name facefusion python=3.12 pip=25.0
```

Cuando pregunte `Proceed ([y]/n)?` escribe **`y`** y presiona Enter.

**Nota:** Si te pide aceptar los Términos de Servicio, escribe **`a`** (accept) y presiona Enter.

---

### **PASO 4: Activar el Entorno**

```cmd
conda activate facefusion
```

Tu prompt debería cambiar de `(base)` a `(facefusion)`.

---

### **PASO 5: Instalar CUDA y cuDNN**

⚠️ **Importante:** Este paso descarga ~1.5-2 GB y puede tardar 5-15 minutos.

```cmd
conda install nvidia/label/cuda-12.9.1::cuda-runtime nvidia/label/cudnn-9.10.0::cudnn
```

Cuando pregunte `Proceed ([y]/n)?` escribe **`y`** y presiona Enter.

**Si hay errores de conexión:** Vuelve a ejecutar el mismo comando. Conda intentará reanudar la descarga.

---

### **PASO 6: Instalar Git (si no lo tienes)**

Verifica si tienes Git:
```cmd
git --version
```

**Si aparece un error:**
1. Descarga Git desde: https://git-scm.com/downloads
2. Instala con las opciones por defecto
3. **Cierra y vuelve a abrir Anaconda Prompt**
4. Ejecuta de nuevo: `conda activate facefusion`

---

### **PASO 7: Descargar FaceFusion**

Navega a donde quieres instalar FaceFusion (ejemplo):

```cmd
cd /d "F:\PROYECTO IDE\AAA Proyectos ALD\Codelatin"
```

O usa tu carpeta preferida. Luego clona el repositorio:

```cmd
git clone https://github.com/facefusion/facefusion
cd facefusion
```

---

### **PASO 8: Instalar FaceFusion con Soporte CUDA**

```cmd
python install.py --onnxruntime cuda
```

Este comando instalará:
- `gradio-rangeslider==0.0.8`
- `gradio==5.44.1`
- `numpy==2.2.6`
- `onnx==1.19.1`
- `onnxruntime-gpu==1.23.2` ← **Importante: versión GPU con CUDA**
- `opencv-python==4.12.0.88`
- `psutil==7.1.3`
- `tqdm==4.67.1`
- `scipy==1.16.3`
- Y muchas más dependencias...

⏱️ Este paso descarga ~400 MB y tarda 5-10 minutos.

---

### **PASO 9: Ejecutar FaceFusion**

```cmd
python facefusion.py run --open-browser
```

La primera vez descargará modelos de IA adicionales (~1 GB) y luego abrirá automáticamente tu navegador en `http://127.0.0.1:7860`.

---

## 📂 Estructura de Archivos

```
Tu Sistema:
├── C:\Users\TU_USUARIO\miniconda3\
│   └── envs\
│       └── facefusion\          ← Entorno virtual (Python + librerías)
│
└── F:\PROYECTO IDE\AAA Proyectos ALD\Codelatin\
    └── facefusion\              ← Código de FaceFusion
        ├── facefusion.py
        ├── install.py
        ├── requirements.txt
        └── ...
```

---

## 🔄 Uso Diario

### **Iniciar FaceFusion**

1. Abre **Anaconda Prompt (miniconda3)**
2. Ejecuta estos comandos:

```cmd
conda activate facefusion
cd /d "F:\PROYECTO IDE\AAA Proyectos ALD\Codelatin\facefusion"
python facefusion.py run --open-browser
```

### **Cerrar FaceFusion**

En Anaconda Prompt, presiona: **`Ctrl + C`**

### **Desactivar el Entorno**

```cmd
conda deactivate
```

---

## 🔧 Gestión del Entorno Conda

### **Ver todos los entornos**
```cmd
conda env list
```

### **Ver paquetes instalados en el entorno actual**
```cmd
conda list
```

### **Eliminar el entorno (si necesitas reinstalar)**
```cmd
conda deactivate
conda env remove --name facefusion
```

### **Exportar el entorno completo**
```cmd
conda activate facefusion
conda env export > environment.yml
```

### **Recrear el entorno desde el archivo**
```cmd
conda env create -f environment.yml
```

---

## 📦 Dependencias Principales

### Instaladas por `install.py --onnxruntime cuda`:

| Paquete | Versión | Propósito |
|---------|---------|-----------|
| gradio | 5.44.1 | Interfaz web |
| gradio-rangeslider | 0.0.8 | Control de rangos en UI |
| numpy | 2.2.6 | Operaciones matemáticas |
| onnx | 1.19.1 | Formato de modelos de IA |
| onnxruntime-gpu | 1.23.2 | Motor de inferencia con CUDA |
| opencv-python | 4.12.0.88 | Procesamiento de imágenes/video |
| psutil | 7.1.3 | Monitoreo del sistema |
| scipy | 1.16.3 | Algoritmos científicos |
| tqdm | 4.67.1 | Barras de progreso |

**Nota:** `onnxruntime-gpu` es la versión con soporte CUDA. No confundir con `onnxruntime` (solo CPU).

---

## 🆕 Actualizar FaceFusion

```cmd
conda activate facefusion
cd /d "F:\PROYECTO IDE\AAA Proyectos ALD\Codelatin\facefusion"
git pull
python install.py --onnxruntime cuda
```

---

## ✅ Verificar que CUDA está funcionando

Al ejecutar FaceFusion, en la consola verás:

```
processing: 100%|=================================| 2674/2674 [03:26<00:00, 12.92frame/s, execution_providers=['cuda']]
```

La parte importante es: **`execution_providers=['cuda']`**

Si solo dice `['cpu']`, significa que no está usando la GPU.

---

## 🐛 Solución de Problemas

### **Problema: "conda: no se reconoce como comando"**
**Solución:** Asegúrate de usar **Anaconda Prompt**, no el Command Prompt normal de Windows.

---

### **Problema: Solo usa CPU, no CUDA**
**Solución:** Reinstala con soporte CUDA:
```cmd
conda activate facefusion
cd /d "TU_RUTA\facefusion"
pip uninstall onnxruntime onnxruntime-gpu -y
python install.py --onnxruntime cuda
```

---

### **Problema: Error de conexión al descargar CUDA**
**Solución:** Vuelve a ejecutar el mismo comando. Conda intentará reanudar la descarga:
```cmd
conda install nvidia/label/cuda-12.9.1::cuda-runtime nvidia/label/cudnn-9.10.0::cudnn
```

---

### **Problema: "Se ha forzado la interrupción de una conexión existente"**
**Solución:** Es un problema temporal de red. Espera unos minutos y vuelve a intentar.

---

### **Problema: Drivers NVIDIA desactualizados**
**Solución:** 
1. Ve al Administrador de dispositivos
2. Busca "Adaptadores de pantalla"
3. Click derecho en tu GPU NVIDIA → "Actualizar controlador"
4. O descarga desde: https://www.nvidia.com/Download/index.aspx

---

## 📝 Instalación en Otra Máquina

### **Método 1: Usando este README**
Simplemente sigue todos los pasos de este documento desde el PASO 1.

---

### **Método 2: Exportar/Importar Entorno Completo**

**En la máquina original:**
```cmd
conda activate facefusion
conda env export > facefusion_env.yml
```

**En la máquina nueva:**
1. Instala Miniconda (PASO 1)
2. Copia el archivo `facefusion_env.yml`
3. Ejecuta:
```cmd
conda env create -f facefusion_env.yml
conda activate facefusion
cd /d "TU_RUTA"
git clone https://github.com/facefusion/facefusion
cd facefusion
```

**Nota:** El método 2 solo funciona si ambas máquinas tienen:
- Mismo sistema operativo (Windows 11)
- Misma arquitectura (64-bit)
- GPU NVIDIA compatible con CUDA

---

## 🎯 Características de FaceFusion

- ✅ Face Swap (Intercambio de caras)
- ✅ Face Enhancement (Mejora de rostros)
- ✅ Frame Enhancement (Mejora de frames)
- ✅ Lip Sync (Sincronización de labios)
- ✅ Procesamiento por lotes
- ✅ Soporte para imágenes y videos
- ✅ Aceleración por GPU (CUDA)

---

## 📊 Rendimiento Esperado

**Con RTX 3050 6GB:**
- Resolución 640x360, 25 FPS: ~13 frames/segundo
- Video de 2674 frames: ~4-5 minutos
- Uso de VRAM: 4-5 GB

**Nota:** Videos de mayor resolución consumirán más VRAM y serán más lentos.

---

## ⚠️ Advertencias Importantes

1. **Uso Ético:** FaceFusion es una herramienta poderosa. Úsala responsablemente y respeta la privacidad de las personas.

2. **VRAM Limitada:** Con 6GB de VRAM, evita procesar videos en resoluciones muy altas (>1080p) simultáneamente.

3. **Espacio en Disco:** Los modelos de IA ocupan ~2-3 GB. Asegúrate de tener suficiente espacio.

4. **Actualizaciones:** FaceFusion se actualiza frecuentemente. Revisa el repositorio oficial para nuevas versiones.

---

## 🔗 Enlaces Útiles

- **Repositorio Oficial:** https://github.com/facefusion/facefusion
- **Documentación:** https://docs.facefusion.io/
- **Discord Comunidad:** https://join.facefusion.io
- **Reddit:** https://reddit.com/r/FaceFusion

---

## 📄 Licencia

FaceFusion está bajo licencia MIT. Consulta el archivo LICENSE.md en el repositorio para más detalles.

---

## ✍️ Notas Finales

- Este README fue creado para Windows 11 con GPU NVIDIA RTX 3050
- Versión de FaceFusion: 3.5.2 (Febrero 2026)
- Python: 3.12.12
- CUDA: 12.9.1
- cuDNN: 9.10.0

**¡Instalación exitosa!** Si tienes problemas, revisa la sección de "Solución de Problemas" o consulta la documentación oficial.

---

*Última actualización: Febrero 6, 2026*