# Entrega de ejercicios

He realizado todos los ejercicios. Los links para cada uno de los repositorios se pueden encontrar a continuación.

## Programación concurrente

 - [GIT y multiprocessing](https://github.com/JavierAbollado/prpa_dia1.git)
 - [Sección crítica. Algoritmo de decker](https://github.com/JavierAbollado/prpa_decker.git)
 - [Sección crítica con semáforos](https://github.com/JavierAbollado/CritSectionSem.git)
 - [Práctica 1](https://github.com/JavierAbollado/Practica-1.git)
 - [Práctica 2](https://github.com/JavierAbollado/Practica-2.git)

## Programación Distribuida

 - [Ejercicios de Programación distribuida](https://github.com/JavierAbollado/chats.git)
 - [Ejercicios mqtt](https://github.com/JavierAbollado/Ejercicios-MQTT.git)
 - [Práctica obligatoria distribuida](https://github.com/JavierAbollado/Practica-3.git)

## Programación Paralela

 - [Contar las palabras de "Don Quijote de La Mancha" con Spark](https://github.com/JavierAbollado/Contar-Quijote-Spark.git)
 - [Triciclos en un grafo](https://github.com/JavierAbollado/Triciclos.git)
 - [Práctica Obligatoria Spark](https://github.com/JavierAbollado/Practica-4.git)

# Apuntes | Programación Paralela y Distribuida en Python

 - [Introducción](#id0)
 - [Conceptos Fundamentales](#id1)
 - [Ejemplos con esquemas sencillos](#id2)
 - [Introducción al Problema de los Filósofos y los Tenedores](#id2.2)
 - [PySpark: Introducción y su Importancia en la Programación Paralela](#id3)
 - [Resumen de comandos de terminal linux](#id4)

# Introducción <a name=id0></a>

La programación paralela y distribuida es una disciplina que se enfoca en la ejecución eficiente de tareas simultáneas en sistemas computacionales. Permite mejorar el rendimiento al aprovechar la capacidad de procesamiento de múltiples núcleos o máquinas interconectadas.

Este repositorio tiene como objetivo proporcionar una visión general de la programación paralela y distribuida en Python, utilizando la biblioteca multiprocessing. A continuación, encontrarás definiciones de conceptos clave y una lista de temas relacionados.

# Conceptos Fundamentales <a name=id1></a>

 - **Programación Paralela**: Se refiere a la ejecución simultánea de tareas en múltiples hilos o procesos con el objetivo de acelerar el tiempo de ejecución. Los hilos o procesos pueden comunicarse y coordinarse entre sí para realizar tareas de manera eficiente.

 - **Programación Distribuida**: Implica la ejecución de tareas en varios dispositivos o máquinas interconectadas en una red. Los programas distribuidos se ejecutan en paralelo, donde cada máquina realiza una parte del trabajo y se comunica con otras máquinas para intercambiar datos y coordinar la ejecución.

- **Multiprocessing**: La biblioteca multiprocessing de Python proporciona una interfaz para crear y controlar procesos, permitiendo la ejecución paralela de tareas en sistemas multi-core. Utiliza el modelo de programación basado en procesos, donde los procesos se ejecutan de forma independiente y se comunican mediante la compartición de datos.

- **Semaforos**: Un semáforo es un mecanismo de sincronización que permite controlar el acceso a recursos compartidos entre múltiples hilos o procesos. Proporciona una forma de garantizar la exclusión mutua y prevenir condiciones de carrera al limitar el número de hilos o procesos que pueden acceder a un recurso al mismo tiempo.

- **Locks**: Los locks (bloqueos) son mecanismos de sincronización que permiten a los hilos o procesos adquirir o liberar acceso exclusivo a un recurso compartido. Un lock puede ser adquirido por un solo hilo o proceso a la vez, evitando que otros accedan al recurso hasta que el lock se libere.

Aparte tenemos definiciones adicionales que te ayudarán a comprender mejor los conceptos clave relacionados con la programación paralela y distribuida, y cómo abordar desafíos como las condiciones de carrera, el interbloqueo, la inanición y el balanceo de carga.

 - **Deadlock (Interbloqueo)**: Es una situación en la que dos o más procesos o hilos quedan atrapados permanentemente esperando recursos que nunca se liberan. Cada proceso o hilo retiene un recurso mientras espera que se libere otro recurso en posesión de otro proceso o hilo, lo que provoca una parálisis en el sistema.

 - **Inanición (Starvation)**: Es un problema que ocurre cuando un proceso o hilo no puede avanzar o no puede acceder a los recursos necesarios debido a que otros procesos o hilos tienen prioridad sobre él. El proceso o hilo "hambriento" queda relegado continuamente, sin obtener los recursos necesarios para su ejecución.

 - **Condiciones de carrera (Race Conditions)**: Se refiere a la situación en la que el resultado de una operación depende del orden y la sincronización de los eventos concurrentes. Ocurre cuando múltiples procesos o hilos acceden simultáneamente a un recurso compartido y el resultado final puede variar según el orden en que se realicen las operaciones.

 - **Exclusión mutua**: Es un mecanismo que garantiza que dos o más procesos o hilos no puedan acceder simultáneamente a un recurso compartido. La exclusión mutua se logra utilizando técnicas como locks, semáforos o monitores para permitir que solo un proceso o hilo acceda al recurso en un momento dado.

 - **Sincronización**: Se refiere a los mecanismos utilizados para coordinar el acceso y la ejecución de múltiples procesos o hilos, evitando problemas como las condiciones de carrera o el interbloqueo. La sincronización puede lograrse mediante semáforos, locks, variables de condición u otras estructuras de datos que faciliten la comunicación y la cooperación entre los procesos o hilos.

 - **Balanceo de carga (Load Balancing)**: Es una técnica que distribuye la carga de trabajo de manera equitativa entre varios procesos o máquinas en un sistema paralelo o distribuido. El objetivo es aprovechar eficientemente los recursos disponibles y evitar situaciones en las que algunos procesos o máquinas estén sobrecargados mientras otros están inactivos.

# Ejemplos con esquemas sencillos <a name=id2></a>

### Multiprocessing 

La biblioteca multiprocessing en Python proporciona soporte para la ejecución de código en paralelo utilizando múltiples procesos. Puedes utilizar esta biblioteca para dividir una tarea en partes más pequeñas y ejecutarlas simultáneamente en varios núcleos de CPU.

Ejemplo de código (cálculo de la suma de números):

```python
from multiprocessing import Pool

def calcular_suma(n):
    return sum(range(1, n+1))

if __name__ == '__main__':
    numeros = [100000, 200000, 300000, 400000]
    with Pool(processes=4) as pool:
        resultados = pool.map(calcular_suma, numeros)
    print(resultados)
```

Otro pequeño ejemplo puede ser sobre el cálculo de la multiplicación de matrices grandes:

```python
import numpy as np
from multiprocessing import Pool

def multiplicar_fila(matriz_a, matriz_b, fila):
    resultado = np.dot(matriz_a[fila], matriz_b)
    return resultado

if __name__ == '__main__':
    matriz_a = np.random.rand(1000, 1000)
    matriz_b = np.random.rand(1000, 1000)

    filas = range(matriz_a.shape[0])

    with Pool() as pool:
        resultados = pool.starmap(multiplicar_fila, [(matriz_a, matriz_b, fila) for fila in filas])

    matriz_resultado = np.vstack(resultados)
    print(matriz_resultado)
```

 ### Sincronización con semáforos
 
Los semáforos son una técnica de sincronización utilizada para controlar el acceso a recursos compartidos en un entorno multihilo. Puedes utilizar la clase Semaphore del módulo multiprocessing para implementar semáforos en Python.

Ejemplo de código (uso de semáforo para controlar acceso a un recurso compartido):

```python
from multiprocessing import Semaphore, Process
import time

semaforo = Semaphore(1)
recurso_compartido = []

def proceso1():
    semaforo.acquire()
    recurso_compartido.append('Datos del proceso 1')
    semaforo.release()

def proceso2():
    semaforo.acquire()
    recurso_compartido.append('Datos del proceso 2')
    semaforo.release()

if __name__ == '__main__':
    p1 = Process(target=proceso1)
    p2 = Process(target=proceso2)
    p1.start()
    p2.start()
    p1.join()
    p2.join()
    print(recurso_compartido)
```

Otro ejemplo puede ser el famoso problema de los "Lectores-Escritores":

```python
import time
from multiprocessing import Semaphore, Process

semaforo_lectores = Semaphore(1)
semaforo_escritores = Semaphore(1)
lectores = 0
escritores = 0

def lector():
    global lectores
    while True:
        semaforo_lectores.acquire()
        lectores += 1
        if lectores == 1:
            semaforo_escritores.acquire()
        semaforo_lectores.release()

        # Realizar operaciones de lectura aquí
        print("Lector leyendo...")

        semaforo_lectores.acquire()
        lectores -= 1
        if lectores == 0:
            semaforo_escritores.release()
        semaforo_lectores.release()

        time.sleep(1)

def escritor():
    global escritores
    while True:
        semaforo_escritores.acquire()
        escritores += 1
        if escritores == 1:
            semaforo_lectores.acquire()
        semaforo_escritores.release()

        # Realizar operaciones de escritura aquí
        print("Escritor escribiendo...")

        semaforo_escritores.acquire()
        escritores -= 1
        if escritores == 0:
            semaforo_lectores.release()
        semaforo_escritores.release()

        time.sleep(1)

if __name__ == '__main__':
    for _ in range(2):
        Process(target=lector).start()

    for _ in range(2):
        Process(target=escritor).start()
```

### Locks

Los locks (bloqueos) son mecanismos de sincronización que permiten a los hilos o procesos adquirir o liberar acceso exclusivo a un recurso compartido. Puedes utilizar la clase Lock del módulo multiprocessing para implementar locks en Python.

Ejemplo de código (uso de lock para controlar acceso a un recurso compartido):

```python
from multiprocessing import Lock, Process

lock = Lock()
recurso_compartido = []

def proceso1():
    with lock:
        recurso_compartido.append('Datos del proceso 1')

def proceso2():
    with lock:
        recurso_compartido.append('Datos del proceso 2')

if __name__ == '__main__':
    p1 = Process(target=proceso1)
    p2 = Process(target=proceso2)
    p1.start()
    p2.start()
    p1.join()
    p2.join()
    print(recurso_compartido)
```

También podemos hacer un hilo productor y consumidor con un búfer compartido:

```python
import time
import random
from multiprocessing import Lock, Process, Queue

lock = Lock()
buffer_compartido = Queue(maxsize=5)

def productor():
    while True:
        item = random.randint(1, 100)
        buffer_compartido.put(item)
        print("Productor produce:", item)
        time.sleep(1)

def consumidor():
    while True:
        item = buffer_compartido.get()
        print("Consumidor consume:", item)
        time.sleep(2)

if __name__ == '__main__':
    Process(target=productor).start()
    Process(target=consumidor).start()
``` 






# Introducción al Problema de los Filósofos y los Tenedores <a name=id2.2></a>

El problema de los filósofos y los tenedores es un clásico problema de concurrencia que ilustra los desafíos de la sincronización en entornos multi-hilo o multi-proceso. Se basa en la situación hipotética en la que varios filósofos se sientan alrededor de una mesa redonda y cada uno necesita tenedores para comer su comida. Sin embargo, solo hay un tenedor entre cada par de filósofos adyacentes.

El desafío radica en evitar los posibles bloqueos y la inanición de los filósofos, asegurando que cada filósofo pueda obtener los dos tenedores necesarios para comer sin interferir con los demás.

### Ejemplo de Código en Python utilizando multiprocessing

A continuación, te presento un ejemplo de código en Python que aborda el problema de los filósofos y los tenedores utilizando el módulo **multiprocessing**. Este código utiliza semáforos para controlar el acceso a los tenedores:

```python
import time
from multiprocessing import Process, Lock, Semaphore

# Número de filósofos
NUM_FILOSOFOS = 5

# Semáforo para controlar el acceso a los tenedores
tenedores = [Semaphore(1) for _ in range(NUM_FILOSOFOS)]

def filosofo(filosofo_id, tenedor_izquierdo, tenedor_derecho):
    while True:
        # Pensar
        print(f"Filósofo {filosofo_id} está pensando.")
        time.sleep(2)

        # Tomar tenedores
        tenedor_izquierdo.acquire()
        tenedor_derecho.acquire()
        print(f"Filósofo {filosofo_id} ha tomado los tenedores y está comiendo.")

        # Comer
        time.sleep(3)
        print(f"Filósofo {filosofo_id} ha terminado de comer.")

        # Soltar tenedores
        tenedor_izquierdo.release()
        tenedor_derecho.release()

if __name__ == "__main__":
    # Crear los procesos de los filósofos
    procesos_filosofos = []
    for i in range(NUM_FILOSOFOS):
        tenedor_izquierdo = tenedores[i]
        tenedor_derecho = tenedores[(i + 1) % NUM_FILOSOFOS]
        proceso = Process(target=filosofo, args=(i, tenedor_izquierdo, tenedor_derecho))
        procesos_filosofos.append(proceso)
        proceso.start()

    # Esperar a que todos los procesos terminen
    for proceso in procesos_filosofos:
        proceso.join()
```

En este ejemplo, cada filósofo es representado por un proceso separado y los tenedores son controlados por semáforos para evitar situaciones de bloqueo. Cada filósofo alterna entre períodos de pensamiento, toma de tenedores, comer y liberación de tenedores.

Este es solo un enfoque para resolver el problema de los filósofos y los tenedores utilizando el módulo **multiprocessing**. Hay otras estrategias y enfoques posibles, pero este código proporciona una base para comprender el concepto y comenzar a explorar más sobre programación paralela y distribuida en Python.




# PySpark: Introducción y su Importancia en la Programación Paralela <a name=id3></a>

PySpark es la interfaz de programación de Python para Apache Spark, un framework de procesamiento de datos distribuido y de alto rendimiento. PySpark permite aprovechar la capacidad de cómputo paralelo de Spark utilizando la potencia de Python como lenguaje de programación.

## Importancia de PySpark en la Programación Paralela

La programación paralela es fundamental en el procesamiento de grandes volúmenes de datos y en el análisis de datos distribuidos. PySpark ofrece las siguientes ventajas:

1. **Procesamiento distribuido**: PySpark permite realizar operaciones en paralelo en un clúster de computadoras, lo que acelera significativamente el procesamiento de datos y reduce los tiempos de ejecución.

2. **Escalabilidad**: PySpark se puede escalar fácilmente para manejar conjuntos de datos cada vez más grandes y cargas de trabajo más exigentes, utilizando recursos distribuidos de manera eficiente.

3. **Programación sencilla**: PySpark proporciona una interfaz de programación sencilla y familiar para los desarrolladores de Python, lo que facilita la escritura y el mantenimiento de código.

4. **Integración con ecosistema de Spark**: PySpark se integra sin problemas con el ecosistema de Spark, lo que permite utilizar otras bibliotecas y herramientas de Spark para el procesamiento de datos, el análisis estadístico, el aprendizaje automático y más.

## Instalación y Ejemplo de Uso de PySpark

Para utilizar PySpark, es necesario tener instalado Apache Spark en el entorno. A continuación se presentan los pasos básicos para la instalación:

1. Descargar e instalar Apache Spark desde el sitio web oficial de Apache Spark (https://spark.apache.org/downloads.html).

2. Configurar las variables de entorno necesarias, como `SPARK_HOME`, que apunte al directorio de instalación de Spark, y `PYTHONPATH`, que incluya la ruta al directorio de la biblioteca PySpark.

Una vez instalado, puedes utilizar PySpark en tus proyectos. A continuación se muestra un ejemplo simple de conteo de palabras utilizando PySpark:

```python
from pyspark.sql import SparkSession

# Crear una sesión de Spark
spark = SparkSession.builder.appName("Conteo de Palabras").getOrCreate()

# Cargar datos desde un archivo
datos = spark.read.text("archivo.txt").rdd.map(lambda x: x[0])

# Realizar el conteo de palabras
conteo = datos.flatMap(lambda x: x.split(" ")).countByValue()

# Mostrar los resultados
for palabra, contador in conteo.items():
    print("{}: {}".format(palabra, contador))
```

Este ejemplo ilustra cómo utilizar PySpark para leer un archivo de texto, dividir las líneas en palabras y contar la frecuencia de cada palabra. PySpark se encarga automáticamente de distribuir el procesamiento en el clúster de Spark para obtener resultados rápidos y eficientes.

## Conexión a un Cluster Auxiliar en PySpark

PySpark proporciona la capacidad de conectarse a un clúster auxiliar para aprovechar su capacidad de cómputo. Para establecer la conexión, se deben proporcionar los detalles del clúster, como las direcciones IP y los puertos relevantes.

Una vez conectado al clúster, PySpark permite distribuir las tareas de procesamiento de datos en el clúster.


# Resumen de comandos de terminal linux <a name=id4></a>

### Comandos de Navegación y Gestión de Directorios

- `pwd`: Muestra la ruta del directorio actual.
- `ls`: Lista los archivos y directorios en el directorio actual.
- `cd`: Cambia el directorio actual.
- `mkdir`: Crea uno o varios directorios.

### Comandos de Gestión de Archivos

- `cp`: Copia archivos y directorios.
- `mv`: Mueve o cambia el nombre de archivos y directorios.
- `rm`: Elimina archivos y directorios.
- `touch`: Crea un nuevo archivo vacío.
- `cat`: Muestra el contenido de un archivo.
- `head`: Muestra las primeras líneas de un archivo.
- `tail`: Muestra las últimas líneas de un archivo.

### Comandos de Gestión de Usuarios y Permisos

- `sudo`: Ejecuta un comando con privilegios de superusuario.
- `useradd`: Crea un nuevo usuario.
- `passwd`: Cambia la contraseña de un usuario.
- `chown`: Cambia el propietario de un archivo o directorio.
- `chmod`: Cambia los permisos de un archivo o directorio.

### Comandos de Red y Conectividad

- `ping`: Envía un paquete ICMP a una dirección IP para verificar la conectividad.
- `ifconfig`: Muestra la configuración de red de las interfaces de red.
- `ssh`: Inicia una sesión segura de shell remota en un servidor.
- `scp`: Copia archivos de forma segura entre hosts locales y remotos.
- `rsync`: Sincroniza archivos y directorios de forma eficiente entre hosts locales y remotos.

