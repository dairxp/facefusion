# Configuración de GPU (NVIDIA CUDA)

## Descripción
Este documento explica cómo configurar FaceFusion para usar tu tarjeta gráfica NVIDIA RTX 3050 con CUDA para acelerar el procesamiento.

## Requisitos
- ✅ Tarjeta gráfica NVIDIA (RTX 3050 o superior)
- ✅ Driver NVIDIA instalado
- ✅ CUDA Toolkit 13.0 o compatible
- ✅ cuDNN instalado

## Verificar la GPU

### 1. Verificar que tienes GPU disponible
```bash
nvidia-smi
```

Deberías ver algo como:
```
NVIDIA GeForce RTX 3050 with Max-Q Design
CUDA Version: 13.0
```

## Instalación

### 1. Desinstalar versión CPU
Si ya instalaste `onnxruntime` (versión CPU):
```bash
uv pip uninstall onnxruntime
```

### 2. Instalar versión GPU
```bash
uv pip uninstall onnxruntime-gpu
uv pip install onnxruntime-gpu==1.20.0
```

## Verificar que FaceFusion detecta la GPU

### 1. Iniciar FaceFusion
```bash
python facefusion.py run
```

### 2. En la interfaz web (http://127.0.0.1:7860)
- Ir a **"EXECUTION PROVIDERS"**
- Deberías ver: `cuda`, `tensorrt`, `cpu`
- Selecciona **`cuda`** para usar GPU

### 3. Confirmar durante procesamiento
En otra terminal, monitorea el uso de GPU:
```bash
nvidia-smi
```

Si ves **GPU-Util > 0%**, ¡estás usando GPU! ✅

## Rendimiento esperado

Con GPU (RTX 3050):
- **Face Swapping**: 10-20 fps en 720p
- **Face Enhancement**: 5-10x más rápido que CPU
- **Processing**: Significativamente acelerado

Sin GPU (CPU):
- Mucho más lento (depende del procesador)

## Solución de problemas

### ❌ "CUDA not available" o no aparece en EXECUTION PROVIDERS
1. Verifica: `nvidia-smi` funciona
2. Reinstala: `uv pip install --force-reinstall onnxruntime-gpu==1.23.2`
3. Reinicia FaceFusion

### ❌ Error de memoria (OOM)
Reduce la resolución o activa **VIDEO MEMORY STRATEGY** en la interfaz

### ❌ Sigue siendo lento
Asegúrate de que seleccionaste **`cuda`** en EXECUTION PROVIDERS

## Cambiar a CPU (si necesitas)
```bash
uv pip uninstall onnxruntime-gpu
uv pip install onnxruntime==1.23.2
```

---

**Última actualización**: 3 de Febrero, 2026  
**Hardware**: NVIDIA GeForce RTX 3050 + CUDA 13.0
