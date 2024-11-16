# GestampChallenge
Obtención de graficas en base a los KPIs principales de varios PDFs

# Procesamiento de Documentos con Azure AI

Este proyecto está diseñado para procesar documentos PDF y extraer información estructurada, como tablas, utilizando las capacidades del servicio **Azure Form Recognizer**. 

## Descripción del Proyecto

El código realiza las siguientes tareas:

1. **Instalación de librerías**: Configuración de todas las dependencias necesarias para ejecutar el proyecto.
2. **Conexión con Azure AI**: Configuración del cliente de Azure Form Recognizer para interactuar con los servicios cognitivos.
3. **Extracción de datos de PDFs**: Procesamiento de documentos PDF para extraer datos tabulares y convertirlos a formato JSON.
4. **Transformación de datos tabulares**: Conversión de los datos extraídos en DataFrames utilizando la biblioteca Pandas.
5. **Análisis de la información**: Preparación de los datos para análisis avanzados o integraciones con otros sistemas.

## Casos de Uso

Este proyecto es útil en escenarios como:

- Digitalización de documentos financieros o empresariales.
- Generación de resúmenes automatizados a partir de datos tabulares.
- Análisis de datos estructurados para informes o reportes.

## Configuración Inicial

### Requisitos

- **Python** 3.7 o superior.
- Una cuenta activa de **Azure** con acceso a los servicios cognitivos.

### Instalación de Dependencias

Ejecuta el siguiente comando para instalar las dependencias necesarias:

```bash
pip install openai azure-ai-formrecognizer azure-ai-textanalytics azure-ai-vision-imageanalysis faiss-cpu pandas
```

### Configuración del Cliente de Azure

Define las siguientes variables en tu código para conectar con Azure:

- `endpoint`: El endpoint de tu servicio Azure Cognitive.
- `key`: La clave de acceso a tu servicio.

Ejemplo:

```python
endpoint = "https://<tu-endpoint>.cognitive.microsoft.com/"
key = "<tu-clave>"
```

## Uso del Proyecto

1. **Clonar el repositorio**:

   ```bash
   git clone https://github.com/tu_usuario/tu_repositorio.git
   ```

2. **Configurar las rutas de entrada y salida**:

   Define las rutas donde se encuentran tus documentos PDF y donde quieres guardar los resultados JSON.

   ```python
   input_path = "ruta/a/los/pdf"
   output_path = "ruta/a/los/json"
   ```

3. **Ejecutar el script de procesamiento**:

   Procesa los documentos PDF y genera archivos JSON con los datos tabulares.

4. **Análisis de datos**:

   Usa las herramientas incluidas para analizar los datos tabulares y convertirlos a DataFrames de Pandas para un análisis más detallado.

## Ejemplo de Código

```python
# Analizar un PDF y guardar resultados
for pdf_file in os.listdir(input_path):
    if pdf_file.endswith(".pdf"):
        file_path = os.path.join(input_path, pdf_file)
        with open(file_path, "rb") as f:
            poller = document_analysis_client.begin_analyze_document("prebuilt-layout", document=f)
            layout = poller.result()
        json_file_path = os.path.join(output_path, pdf_file.replace(".pdf", ".json"))
        with open(json_file_path, 'w') as fp:
            json.dump(layout.to_dict(), fp)
