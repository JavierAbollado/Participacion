# Programación Paralela y Distribuida en Python

La programación paralela y distribuida es una disciplina que se enfoca en la ejecución eficiente de tareas simultáneas en sistemas computacionales. Permite mejorar el rendimiento al aprovechar la capacidad de procesamiento de múltiples núcleos o máquinas interconectadas.

Este repositorio tiene como objetivo proporcionar una visión general de la programación paralela y distribuida en Python, utilizando la biblioteca multiprocessing. A continuación, encontrarás definiciones de conceptos clave y una lista de temas relacionados.

## Conceptos Fundamentales

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

## Ejemplos con esquemas sencillos

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





