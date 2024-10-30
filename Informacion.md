# Documentación del Proyecto de Streaming con Spark y Kafka

## Instalación de Dependencias
Se instaló pyspark en un entorno virtual para evitar conflictos de permisos y dependencias con el sistema:
```bash
python3 -m venv myenv
source myenv/bin/activate
pip install pyspark
```

## Archivo de Streaming
Se creó un archivo llamado streaming_vuelos.py con el siguiente contenido:
```bash
from pyspark import SparkContext
from pyspark.streaming import StreamingContext
from pyspark.streaming.kafka import KafkaUtils

# Crear un contexto de Spark
sc = SparkContext("local[*]", "KafkaStreamingApp")
ssc = StreamingContext(sc, 5)  # Cada 5 segundos

# Conectar a Kafka
kafkaStream = KafkaUtils.createStream(ssc, 'localhost:2181', 'spark-streaming', {'vuelos': 1})

# Procesar los datos
def process_message(message):
    print("Mensaje recibido:", message)

# Para cada RDD en el stream, procesar los mensajes
kafkaStream.foreachRDD(lambda rdd: rdd.foreach(process_message))

# Iniciar el contexto
ssc.start()
ssc.awaitTermination()
```
## Ejecución del Script
Al ejecutar el script, se presentaron varios problemas:

### - Error de Sintaxis
Hubo un error de sintaxis en la línea que crea la conexión a Kafka debido a un carácter incompleto.

### - Errores de Importación
Tras corregir la línea de conexión a Kafka, se presentó un error relacionado con la instalación de pyspark:
```bash
TypeError: 'bytes' object cannot be interpreted as an integer
```

Esto sugiere que puede haber un problema con la versión de pyspark o incompatibilidades con Python.

## Comprobación de Kafka
Se intentó listar los temas de Kafka, pero se encontró un error debido a la falta del parámetro --zookeeper, ya que las versiones más recientes de Kafka no requieren Zookeeper para algunos comandos.
Para listar los temas, usa:

```bash
bin/kafka-topics.sh --list --bootstrap-server localhost:9092
```

## Inicio de Zookeeper y Kafka
Al intentar iniciar Zookeeper y Kafka, se recibieron mensajes de error indicando que los scripts no estaban localizados:

```bash
bash: bin/zookeeper-server-start.sh: No such file or directory
```

## Solución:
Se aseguro la correcto ubicacion en los directorios donde están los scripts de Kafka, se confirmo que los servicios y los entornos se encontraran activos, se verifica que en los datos registrados se hallan guardado de forma correcta, se realiza envio de prueba directamente desde Kafka y se confirma el ingreso en Spark 
