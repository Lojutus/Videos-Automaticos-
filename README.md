📹 Proyecto de Creación de Videos Automáticos desde YouTube
Este proyecto automatiza la creación de videos estilizados a partir de audios o videos descargados de YouTube, generando imágenes sincronizadas y animaciones llamativas usando Python, Whisper, WhisperX, Pillow y FFmpeg.
🛠️ Origen del Proyecto
La primera parte del proyecto —que incluye la descarga de videos de YouTube usando pytube y la transcripción automática usando Whisper— fue adaptada inicialmente de un cuaderno de Colab genérico encontrado en internet.
Por esa razón, en esa sección es posible encontrar comentarios en inglés o fragmentos de código que no siguen exactamente el mismo estilo del resto del proyecto.

Estos comentarios heredados no afectan el funcionamiento, pero a futuro podría ser buena idea limpiar y unificar todo el código para que sea más coherente y esté 100% documentado en español.

Posteriormente, el resto del flujo (procesamiento de palabras, generación de imágenes con Pillow y ensamblaje de video con ffmpeg) fue desarrollado de manera personalizada para adaptarse al objetivo final del proyecto.
☁️Trabajo en Google Colab
Todo el desarrollo de este proyecto se realizó en Google Colab para aprovechar su entorno basado en la nube, acceso rápido a GPUs (si es necesario) y facilidad de compartir.
Por esta razón, el flujo completo (descarga de videos, transcripción, generación de imágenes y creación del video final) está organizado en un cuaderno en formato .ipynb (Jupyter Notebook), lo cual permite:

Ejecutar paso por paso de manera ordenada.

Visualizar resultados intermedios (por ejemplo, imágenes generadas o fragmentos de transcripción).

Modificar parámetros rápidamente sin tener que ejecutar todo desde cero.

Si deseas trabajar de manera local, también puedes exportar el .ipynb a un script .py estándar, aunque es recomendado mantenerlo en notebook para facilitar la interacción.


🚀 ¿Qué hace el proyecto?
Descarga de Video o Audio de YouTube
Se descarga el audio de un video usando herramientas como yt-dlp o pytube.

Transcripción del Audio
Se transcribe el audio usando Whisper (modelo de OpenAI) para obtener el texto en formato .srt (subtítulos) o texto plano.

Alineación de Palabras
Con WhisperX se alinea cada palabra con su tiempo exacto de inicio y fin, generando un archivo .json (alineación por palabra).

Generación de Metadata Visual
Se crea un archivo visual_metadata.json que organiza palabra por palabra indicando:

Texto

Estilo visual (tipo de filtro)

Fuente tipográfica

Duración

A qué frase pertenece

Renderizado de Imágenes por Frase (usando Pillow)
Para cada palabra o grupo de palabras:

Se genera una imagen .png de alta calidad usando Pillow.

El texto se centra automáticamente y respeta el número máximo de palabras por línea.

Se aplican estilos diferentes según el tipo de palabra.

Se guarda un metadata.json con los datos de sincronización de cada imagen.

Creación de Video Final (usando FFmpeg)
Finalmente, se combinan:

Las imágenes generadas

El audio original Para producir un video sincronizado donde el texto aparece de forma animada al ritmo del audio.

🧩 Estructura del Proyecto:
/data
    audio.mp3          # Audio descargado
    audio.srt          # Subtítulos generados
    audio.aligned.json # Alineación palabra por palabra
    visual_metadata.json # Metadata visual generada

/output
    /frase_0000/
        palabra_000.png
        palabra_001.png
        metadata.json
    /frase_0001/
        ...

⚙️ Tecnologías utilizadas
Python 3.9+

Whisper (transcripción)

WhisperX (alineación precisa)

Pillow (renderizado de imágenes)

FFmpeg (ensamblado de video)

yt-dlp (descarga de audio/video)

json (manejo de metadata)
📋 Requisitos
Python 3.9 o superior

Paquetes:

openai-whisper

whisperx

pillow

ffmpeg-python

yt-dlp

pytube

FFmpeg instalado en el sistema (apt install ffmpeg en Linux o brew install ffmpeg en Mac).
🚧 Notas importantes
Todo el sistema está preparado para videos verticales (1080x1920) tipo TikTok o Instagram Reels.

El renderizado de imágenes usa Pillow y no HTML ni navegadores.

Se puede personalizar:

Tipo de fuente (.ttf)

Colores de fondo y texto

Tamaño máximo de palabras por línea

Estilos visuales para palabras destacadas
