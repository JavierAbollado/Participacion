# Programación Paralela y Distribuida en Python

La programación paralela y distribuida es una disciplina que se enfoca en la ejecución eficiente de tareas simultáneas en sistemas computacionales. Permite mejorar el rendimiento al aprovechar la capacidad de procesamiento de múltiples núcleos o máquinas interconectadas.

Este repositorio tiene como objetivo proporcionar una visión general de la programación paralela y distribuida en Python, utilizando la biblioteca multiprocessing. A continuación, encontrarás definiciones de conceptos clave y una lista de temas relacionados.

## Definiciones

 - **Programación Paralela**: Se refiere a la ejecución simultánea de tareas en múltiples hilos o procesos con el objetivo de acelerar el tiempo de ejecución. Los hilos o procesos pueden comunicarse y coordinarse entre sí para realizar tareas de manera eficiente.

 - **Programación Distribuida**: Implica la ejecución de tareas en varios dispositivos o máquinas interconectadas en una red. Los programas distribuidos se ejecutan en paralelo, donde cada máquina realiza una parte del trabajo y se comunica con otras máquinas para intercambiar datos y coordinar la ejecución.

- **Multiprocessing**: La biblioteca multiprocessing de Python proporciona una interfaz para crear y controlar procesos, permitiendo la ejecución paralela de tareas en sistemas multi-core. Utiliza el modelo de programación basado en procesos, donde los procesos se ejecutan de forma independiente y se comunican mediante la compartición de datos.

- **Semaforos**: Un semáforo es un mecanismo de sincronización que permite controlar el acceso a recursos compartidos entre múltiples hilos o procesos. Proporciona una forma de garantizar la exclusión mutua y prevenir condiciones de carrera al limitar el número de hilos o procesos que pueden acceder a un recurso al mismo tiempo.

- **Locks**: Los locks (bloqueos) son mecanismos de sincronización que permiten a los hilos o procesos adquirir o liberar acceso exclusivo a un recurso compartido. Un lock puede ser adquirido por un solo hilo o proceso a la vez, evitando que otros accedan al recurso hasta que el lock se libere.


## Ejemplos sencillos

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








