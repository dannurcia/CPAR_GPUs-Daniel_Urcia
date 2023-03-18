# Evaluación del curso "Computación Paralela con GPU's"

**AUTOR: Daniel A. Urcia Paredes**

A continuación, se desarrollan cada una de las actividades solicitadas.

## 0. Clonar el repositorio "oneAPI-samples" [1 punto]

Para ello, se accederá a través de los comandos que nos ofrece git. Primero, veremos la ubicación actual:

`!cd /home/u185959`

Procediendo a clonar con "git clone"

`!git clone https://github.com/oneapi-src/oneAPI-samples`

```
Cloning into 'oneAPI-samples'...
remote: Enumerating objects: 24959, done.
remote: Counting objects: 100% (419/419), done.
remote: Compressing objects: 100% (276/276), done.
remote: Total 24959 (delta 176), reused 328 (delta 134), pack-reused 24540
Receiving objects: 100% (24959/24959), 256.67 MiB | 3.56 MiB/s, done.
Resolving deltas: 100% (16320/16320), done.
Updating files:  45% (1556/3457)
```

## 1. Cambiar al directorio del ejemplo "NBody" [1 punto]
- Directorio: `oneAPI-samples/tree/master/DirectProgramming/C++SYCL/N-BodyMethods/Nbody`

Para ellos cambiamos el directorio con el comando "cd"

`cd oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody`

```
/home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody
```

Verificando la ubicación actual:

`pwd`

```
'/home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody'
```

## 2. Explicar brevemente el algoritmo de `Nbody` [3 puntos]

El algoritmo de **NBody** refiere a una clase de métodos de simulación que permiten modelar el comportamiento de un sistema físico utilizando un conjunto de entidades discretas como átomos, cuerpos astrofísicos, etc., y un conjunto de interacciones entre ellos denominados **potenciales de acoplamiento**, tales como la fuerza, aceleración, velocidad, posición, entre otros, las cuales dependen del tiempo. Este algoritmo es muy paralelo a los datos, por lo que el código se adecua muy bien para ejecutarlo en un GPU, además demuestra cómo lidiar con varios núcleos de dispositivos que se pueden poner en una cola SYCL para su ejecución.

## 3. Acceder en modo interactivo a un nodo de cómputo con GPUs (`gen9` o `gen11`) [3 puntos]
- Compilar y ejecutar `Nbody`
- Proporcionar screenshot(s) de los resultados
- Por cada screenshot, añadir una breve descripción

En este punto, primero se debe acceder al nodo en modo interactivo, para ello se ha escogido el gen11.

`!qsub -I -l nodes=1:gen11:ppn=2 -d .`

```
qsub: waiting for job 2254252.v-qsvr-1.aidevcloud to start
qsub: job 2254252.v-qsvr-1.aidevcloud ready


########################################################################
#      Date:           Thu 16 Mar 2023 12:11:51 PM PDT
#    Job ID:           2254252.v-qsvr-1.aidevcloud
#      User:           u185959
# Resources:           cput=75:00:00,neednodes=1:gen11:ppn=2,nodes=1:gen11:ppn=2,walltime=06:00:00
########################################################################

]0;u185959@s019-n008: ~/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbodyu185959@s019-n008:~/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody$ 
```
Una vez conectado al nodo, se verificará qué dispositivos soporta:

`!sycl-ls`

```
[opencl:acc:0] Intel(R) FPGA Emulation Platform for OpenCL(TM), Intel(R) FPGA Emulation Device 1.2 [2022.15.12.0.01_081451]
[opencl:cpu:1] Intel(R) OpenCL, Intel(R) Xeon(R) Gold 6128 CPU @ 3.40GHz 3.0 [2022.15.12.0.01_081451]
```

Lo que se observa es que este nodo dispone de un acelerador FPGA y un CPU Intel Xeon.

**Compilando y ejecutando "NBody"**

Construyendo el programa:

`mkdir build`

`cd build`

```
/home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build
!cmake ..
```

`!cmake ..`

```
-- The C compiler identification is GNU 9.4.0
-- The CXX compiler identification is Clang 16.0.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /glob/development-tools/versions/oneapi/2023.0.1/oneapi/compiler/2023.0.0/linux/bin/icpx
-- Check for working CXX compiler: /glob/development-tools/versions/oneapi/2023.0.1/oneapi/compiler/2023.0.0/linux/bin/icpx -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build
```

`!make`

```
Scanning dependencies of target nbody
[ 33%] Building CXX object src/CMakeFiles/nbody.dir/GSimulation.cpp.o
[ 66%] Building CXX object src/CMakeFiles/nbody.dir/main.cpp.o
[100%] Linking CXX executable nbody
[100%] Built target nbody
```

Ejecutando el programa:

`!make run`

```
Scanning dependencies of target run
===============================
 Initialize Gravity Simulation
 nPart = 16000; nSteps = 10; dt = 0.1
------------------------------------------------
 s       dt      kenergy     time (s)    GFLOPS      
------------------------------------------------
 1       0.1     26.405      0.96413     7.7005      
 2       0.2     313.77      0.025533    290.78      
 3       0.3     926.56      0.016176    458.98      
 4       0.4     1866.4      0.015141    490.34      
 5       0.5     3135.6      0.015565    476.98      
 6       0.6     4737.6      0.015174    489.29      
 7       0.7     6676.6      0.015117    491.12      
 8       0.8     8957.7      0.01513     490.72      
 9       0.9     11587       0.016008    463.79      
 10      1       14572       0.015962    465.11      

# Total Time (s)     : 1.1142
# Average Performance : 478.29 +- 12.96
===============================
Built target run
```

**Breves descripciones de los resultados**

CMake a través de sus comando **!cmake ..** y **make**, como sistema de generación de scripts para el entorno de trabajo utilizado genera los archivos necesarios para la ejecución del algoritmo y los guarda en la dirección "/home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build". Luego, permite correr los archivos ejecutables generados anteriormente que contienen el algoritmo **NBody**.

Este algoritmo inicia la simulación de la gravedad con un número de partículas (nPart) igual a 16000, considera también 10 pasos de integración (nSteps) y 
un diferencial de tiempo (dt) igual a 0.1. El cálculo de los parámetros depende de las "nParts-1" partículas restantes. Se observa en la tabla de resultados que, a medida que el tiempo transcurre, el sistema de partículas aumenta su energía y el consumo computacional en promedio aumenta y se acerca a medio teraflop.

## 4. Realizar un análisis de _**GPU Hotspots**_ con VTune [8 puntos]
- Indicar los hotspots del programa
- Proporcionar screenshot(s) de los resultados
- Por cada screenshot, añadir una breve descripción



