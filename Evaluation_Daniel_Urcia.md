---
jupyter:
  kernelspec:
    display_name: Python 3 (Intel® oneAPI 2023.0)
    language: python
    name: c009-intel_distribution_of_python_3\_oneapi-beta05-python
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.9.15
  nbformat: 4
  nbformat_minor: 5
---

::: {#4714164e-62a7-4088-809c-44cecf306484 .cell .markdown}
# Evaluación del curso \"Computación Paralela con GPU\'s\"

**AUTOR: Daniel A. Urcia Paredes**

A continuación, se desarrollan cada una de las actividades solicitadas.
:::

::: {#bec0e9b8-31b4-4a40-a1c1-91c7b6c945b5 .cell .markdown}
## 0. Clonar el repositorio \"oneAPI-samples\" \[1 punto\] {#0-clonar-el-repositorio-oneapi-samples-1-punto}
:::

::: {#41c5b5a7-5866-4903-a34f-712d5e789834 .cell .markdown}
Para ello, se accederá a través de los comandos que nos ofrece git.
Primero, veremos la ubicación actual:
:::

::: {#f735f555-ed08-48f6-8e0b-101be4f794e8 .cell .code execution_count="9"}
``` python
!cd /home/u185959
```
:::

::: {#0f0af2ff-30de-42a5-a061-b84c934d4453 .cell .markdown}
Procediendo a clonar con \"git clone\"
:::

::: {#ce98d149-af2b-4a5d-9de8-52c07769cb01 .cell .code}
``` python
!git clone https://github.com/oneapi-src/oneAPI-samples
```

::: {.output .stream .stdout}
    Cloning into 'oneAPI-samples'...
    remote: Enumerating objects: 24959, done.ote: Counting objects: 100% (419/419), done.ote: Compressing objects: 100% (276/276), done.ote: Total 24959 (delta 176), reused 328 (delta 134), pack-reused 24540
:::
:::

::: {#e753c158-a220-4bb7-860d-c09e7c49e49a .cell .markdown}
## 1. Cambiar al directorio del ejemplo \"NBody\" \[1 punto\] {#1-cambiar-al-directorio-del-ejemplo-nbody-1-punto}

-   Directorio:
    `oneAPI-samples/tree/master/DirectProgramming/C++SYCL/N-BodyMethods/Nbody`
:::

::: {#d76a2265-e327-4585-9dec-53b650c04461 .cell .markdown}
Para ellos cambiamos el directorio con el comando \"cd\"
:::

::: {#685ab9be-e1ff-4edb-bf94-056c12e4cc5e .cell .code execution_count="10"}
``` python
cd oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody
```

::: {.output .stream .stdout}
    /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody
:::
:::

::: {#905275a3-ccb3-461c-a807-f4755c5b1bd2 .cell .markdown}
Verificando la ubicación actual:
:::

::: {#a5c4b1e3-3f0f-4ef2-b9bf-e8dab8dfd085 .cell .code execution_count="11"}
``` python
pwd
```

::: {.output .execute_result execution_count="11"}
    '/home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody'
:::
:::

::: {#b118de32-47b2-45e7-8064-139678ebba8f .cell .markdown}
## 2. Explicar brevemente el algoritmo de `Nbody` \[3 puntos\] {#2-explicar-brevemente-el-algoritmo-de-nbody-3-puntos}
:::

::: {#d00dc699-fc2f-49b8-bfe5-24d7c49d4658 .cell .markdown}
El algoritmo de **NBody** refiere a una clase de métodos de simulación
que permiten modelar el comportamiento de un sistema físico utilizando
un conjunto de entidades discretas como átomos, cuerpos astrofísicos,
etc., y un conjunto de interacciones entre ellos denominados
**potenciales de acoplamiento**, tales como la fuerza, aceleración,
velocidad, posición, entre otros, las cuales dependen del tiempo. Este
algoritmo es muy paralelo a los datos, por lo que el código se adecua
muy bien para ejecutarlo en un GPU, además demuestra cómo lidiar con
varios núcleos de dispositivos que se pueden poner en una cola SYCL para
su ejecución.
:::

::: {#1471bc7f-7a2c-42bb-8a80-0a94afdcd618 .cell .markdown}
## 3. Acceder en modo interactivo a un nodo de cómputo con GPUs (`gen9` o `gen11`) \[3 puntos\] {#3-acceder-en-modo-interactivo-a-un-nodo-de-cómputo-con-gpus-gen9-o-gen11-3-puntos}

-   Compilar y ejecutar `Nbody`
-   Proporcionar screenshot(s) de los resultados
-   Por cada screenshot, añadir una breve descripción
:::

::: {#bade1aa2-f4ca-40c9-894c-b98ec851afef .cell .markdown}
En este punto, primero se debe acceder al nodo en modo interactivo, para
ello se ha escogido el gen11.
:::

::: {#c8e96742-02d5-4c33-9351-ad19dc8bf33d .cell .code}
``` python
!qsub -I -l nodes=1:gen11:ppn=2 -d .
```

::: {.output .stream .stdout}
    qsub: waiting for job 2254252.v-qsvr-1.aidevcloud to start
    qsub: job 2254252.v-qsvr-1.aidevcloud ready


    ########################################################################
    #      Date:           Thu 16 Mar 2023 12:11:51 PM PDT
    #    Job ID:           2254252.v-qsvr-1.aidevcloud
    #      User:           u185959
    # Resources:           cput=75:00:00,neednodes=1:gen11:ppn=2,nodes=1:gen11:ppn=2,walltime=06:00:00
    ########################################################################

    ]0;u185959@s019-n008: ~/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbodyu185959@s019-n008:~/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody$ 
:::
:::

::: {#d92e789e-227d-499d-992d-ed23093bd416 .cell .markdown}
Una vez conectado al nodo, se verificará qué dispositivos soporta:
:::

::: {#ae633127-717e-4b15-8834-fc0815cb7ca9 .cell .code execution_count="1"}
``` python
!sycl-ls
```

::: {.output .stream .stdout}
    [opencl:acc:0] Intel(R) FPGA Emulation Platform for OpenCL(TM), Intel(R) FPGA Emulation Device 1.2 [2022.15.12.0.01_081451]
    [opencl:cpu:1] Intel(R) OpenCL, Intel(R) Xeon(R) Gold 6128 CPU @ 3.40GHz 3.0 [2022.15.12.0.01_081451]
:::
:::

::: {#f8da43f6-6dd2-41d4-959b-4011e085b0ac .cell .markdown}
Lo que se observa es que este nodo dispone de un acelerador FPGA y un
CPU Intel Xeon.
:::

::: {#a5e14588-cf28-48c6-bc67-70f0103ded48 .cell .markdown}
**Compilando y ejecutando \"NBody\"**
:::

::: {#4e2e1443-0e22-44bb-8471-6e3174b248f2 .cell .markdown}
Construyendo el programa:
:::

::: {#94f95f21-be72-4262-9191-ca6b39f0d608 .cell .code execution_count="8"}
``` python
mkdir build
```
:::

::: {#a520bb69-0d35-41ad-a548-598c2ab669a9 .cell .code execution_count="9"}
``` python
cd build
```

::: {.output .stream .stdout}
    /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build
:::
:::

::: {#50139cab-55c9-4cf6-9571-49d6b33b22f3 .cell .code execution_count="11"}
``` python
!cmake ..
```

::: {.output .stream .stdout}
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
:::
:::

::: {#93f98a4b-fb30-46a9-a8a1-a9d31be87e94 .cell .code execution_count="13"}
``` python
!make
```

::: {.output .stream .stdout}
    Scanning dependencies of target nbody
    [ 33%] Building CXX object src/CMakeFiles/nbody.dir/GSimulation.cpp.o
    [ 66%] Building CXX object src/CMakeFiles/nbody.dir/main.cpp.o
    [100%] Linking CXX executable nbody
    [100%] Built target nbody
:::
:::

::: {#f0a64453-043c-48eb-ac27-9b311fc30860 .cell .markdown}
Ejecutando el programa:
:::

::: {#420b5065-f27f-4848-b9b6-8b0f3fc0b8bc .cell .code execution_count="15"}
``` python
!make run
```

::: {.output .stream .stdout}
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
:::
:::

::: {#9d9d91df-a903-4134-b651-d395fd41bf23 .cell .markdown}
**Breves descripciones de los resultados**
:::

::: {#1d124d4e-f655-4de7-ab36-edeedce9302a .cell .markdown}
CMake a través de sus comando **!cmake ..** y **make**, como sistema de
generación de scripts para el entorno de trabajo utilizado genera los
archivos necesarios para la ejecución del algoritmo y los guarda en la
dirección
\"/home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build\".
Luego, permite correr los archivos ejecutables generados anteriormente
que contienen el algoritmo **NBody**.
:::

::: {#aa35e876-99cf-4f88-9884-95bcb16d2112 .cell .markdown}
Este algoritmo inicia la simulación de la gravedad con un número de
partículas (nPart) igual a 16000, considera también 10 pasos de
integración (nSteps) y un diferencial de tiempo (dt) igual a 0.1. El
cálculo de los parámetros depende de las \"nParts-1\" partículas
restantes. Se observa en la tabla de resultados que, a medida que el
tiempo transcurre, el sistema de partículas aumenta su energía y el
consumo computacional en promedio aumenta y se acerca a medio teraflop.
:::

::: {#aff7488d-1f3d-4490-9844-67c8548315a8 .cell .markdown}
## 4. Realizar un análisis de ***GPU Hotspots*** con VTune \[8 puntos\] {#4-realizar-un-análisis-de-gpu-hotspots-con-vtune-8-puntos}

-   Indicar los hotspots del programa
-   Proporcionar screenshot(s) de los resultados
-   Por cada screenshot, añadir una breve descripción
:::

::: {#821d92b4-9679-4e04-9e85-a703621d6297 .cell .markdown}
Para ello, ubicamos el archivo binario generado por la compilacion del
código fuente del algoritmo
:::

::: {#798e26e1-59f2-4d5a-aef6-95886cf755ed .cell .code execution_count="2"}
``` python
!vtune -collect performance-snapshot -- /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/nbody
```

::: {.output .stream .stdout}
    vtune: Peak bandwidth measurement started.
    vtune: Peak bandwidth measurement finished.
    vtune: Collection started. To stop the collection, either press CTRL-C or enter from another console window: vtune -r /home/u185959/computacion_paralela/CPAR_GPUs/r000ps -command stop.
    ===============================
     Initialize Gravity Simulation
     nPart = 16000; nSteps = 10; dt = 0.1
    ------------------------------------------------
     s       dt      kenergy     time (s)    GFLOPS      
    ------------------------------------------------
     1       0.1     26.405      0.76754     9.6728      
     2       0.2     313.77      0.026696    278.1       
     3       0.3     926.56      0.016498    450.02      
     4       0.4     1866.4      0.015813    469.52      
     5       0.5     3135.6      0.015798    469.95      
     6       0.6     4737.6      0.015743    471.58      
     7       0.7     6676.6      0.01578     470.5       
     8       0.8     8957.7      0.015904    466.81      
     9       0.9     11587       0.015812    469.53      
     10      1       14572       0.015564    477.01      

    # Total Time (s)     : 0.9214
    # Average Performance : 468.11 +- 7.3575
    ===============================
    vtune: Collection stopped.
    vtune: Using result path `/home/u185959/computacion_paralela/CPAR_GPUs/r000ps'
    vtune: Executing actions 75 % Generating a report                              Elapsed Time: 4.355s
        IPC: 1.013
        SP GFLOPS: 18.595
        DP GFLOPS: 0.000
        x87 GFLOPS: 0.000
        Average CPU Frequency: 2.536 GHz
    Logical Core Utilization: 2.7% (0.637 out of 24)
     | The metric value is low, which may signal a poor logical CPU cores
     | utilization. Consider improving physical core utilization as the first step
     | and then look at opportunities to utilize logical cores, which in some cases
     | can improve processor throughput and overall performance of multi-threaded
     | applications.
     |
        Physical Core Utilization: 3.3% (0.394 out of 12)
         | The metric value is low, which may signal a poor physical CPU cores
         | utilization caused by:
         |     - load imbalance
         |     - threading runtime overhead
         |     - contended synchronization
         |     - thread/process underutilization
         |     - incorrect affinity that utilizes logical cores instead of physical
         |       cores
         | Run the HPC Performance Characterization analysis to estimate the
         | efficiency of MPI and OpenMP parallelism or run the Locks and Waits
         | analysis to identify parallel bottlenecks for other parallel runtimes.
         |
    Microarchitecture Usage: 43.9% of Pipeline Slots
     | You code efficiency on this platform is too low.
     | 
     | Possible cause: memory stalls, instruction starvation, branch misprediction
     | or long latency instructions.
     | 
     | Next steps: Run Microarchitecture Exploration analysis to identify the cause
     | of the low microarchitecture usage efficiency.
     |
        Retiring: 43.9% of Pipeline Slots
        Front-End Bound: 17.0% of Pipeline Slots
         | Issue: A significant portion of Pipeline Slots is remaining empty due to
         | issues in the Front-End.
         | 
         | Tips:  Make sure the code working size is not too large, the code layout
         | does not require too many memory accesses per cycle to get enough
         | instructions for filling four pipeline slots, or check for microcode
         | assists.
         |
        Bad Speculation: 5.5% of Pipeline Slots
        Back-End Bound: 33.6% of Pipeline Slots
         | A significant portion of pipeline slots are remaining empty. When
         | operations take too long in the back-end, they introduce bubbles in the
         | pipeline that ultimately cause fewer pipeline slots containing useful
         | work to be retired per cycle than the machine is capable to support. This
         | opportunity cost results in slower execution. Long-latency operations
         | like divides and memory operations can cause this, as can too many
         | operations being directed to a single execution port (for example, more
         | multiply operations arriving in the back-end per cycle than the execution
         | unit can support).
         |
            Memory Bound: 8.8% of Pipeline Slots
                L1 Bound: 17.6% of Clockticks
                    FB Full: 49.6% of Clockticks
                L2 Bound: 0.5% of Clockticks
                L3 Bound: 1.7% of Clockticks
                    L3 Latency: 2.5% of Clockticks
                DRAM Bound: 1.3% of Clockticks
                    Memory Bandwidth: 1.8% of Clockticks
                    Memory Latency: 6.5% of Clockticks
                        Local DRAM: 2.6% of Clockticks
                        Remote DRAM: 0.1% of Clockticks
                        Remote Cache: 0.0% of Clockticks
                Store Bound: 1.2% of Clockticks
            Core Bound: 24.9% of Pipeline Slots
             | This metric represents how much Core non-memory issues were of a
             | bottleneck. Shortage in hardware compute resources, or dependencies
             | software's instructions are both categorized under Core Bound. Hence
             | it may indicate the machine ran out of an OOO resources, certain
             | execution units are overloaded or dependencies in program's data- or
             | instruction- flow are limiting the performance (e.g. FP-chained long-
             | latency arithmetic operations).
             |
    Memory Bound: 8.8% of Pipeline Slots
        Cache Bound: 19.8% of Clockticks
        DRAM Bound: 1.3% of Clockticks
            Average DRAM Bandwidth, GB/s: 0.000
        NUMA: % of Remote Accesses: 1.1%
    Vectorization: 100.0% of Packed FP Operations
        Instruction Mix
            SP FLOPs: 66.2% of uOps
                Packed: 100.0% from SP FP
                    128-bit: 0.0% from SP FP
                    256-bit: 0.0% from SP FP
                    512-bit: 100.0% from SP FP
                Scalar: 0.0% from SP FP
            DP FLOPs: 0.0% of uOps
                Packed: 0.0% from DP FP
                    128-bit: 0.0% from DP FP
                    256-bit: 0.0% from DP FP
                    512-bit: 0.0% from DP FP
                Scalar: 100.0% from DP FP
                 | This code has floating point operations and is not vectorized.
                 | Consider either recompiling the code with optimization options
                 | that allow vectorization or using Intel Advisor to vectorize the
                 | loops.
                 |
            x87 FLOPs: 0.0% of uOps
            Non-FP: 33.8% of uOps
        FP Arith/Mem Rd Instr. Ratio: 4.296
        FP Arith/Mem Wr Instr. Ratio: 9.717
    Collection and Platform Info
        Application Command Line: /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/nbody 
        Operating System: 5.4.0-80-generic DISTRIB_ID=Ubuntu DISTRIB_RELEASE=20.04 DISTRIB_CODENAME=focal DISTRIB_DESCRIPTION="Ubuntu 20.04.6 LTS"
        Computer Name: s001-n064
        Result Size: 3.7 MB 
        Collection start time: 21:41:01 16/03/2023 UTC
        Collection stop time: 21:41:06 16/03/2023 UTC
        Collector Type: Driverless Perf per-process counting
        CPU
            Name: Intel(R) Xeon(R) Processor code named Skylake
            Frequency: 3.392 GHz
            Logical CPU Count: 24
            Max DRAM Single-Package Bandwidth: 53.000 GB/s
            LLC size: 20.2 MB 
            Cache Allocation Technology
                Level 2 capability: not detected
                Level 3 capability: available

    Recommendations:
        Hotspots: Start with Hotspots analysis to understand the efficiency of your algorithm.
         | Use Hotspots analysis to identify the most time consuming functions.
         | Drill down to see the time spent on every line of code.
        Threading: There is poor utilization of logical CPU cores (2.7%) in your application.
         |  Use Threading to explore more opportunities to increase parallelism in
         | your application.
        Microarchitecture Exploration: There is low microarchitecture usage (43.9%) of available hardware resources.
         | Run Microarchitecture Exploration analysis to analyze CPU
         | microarchitecture bottlenecks that can affect application performance.

    If you want to skip descriptions of detected performance issues in the report,
    enter: vtune -report summary -report-knob show-issues=false -r <my_result_dir>.
    Alternatively, you may view the report in the csv format: vtune -report
    <report_name> -format=csv.
    vtune: Executing actions 100 % done                                            
:::
:::

::: {#cb95bfb8-c378-47f7-b535-f1f5f48304a6 .cell .markdown}
**Indicando los hotspost del programa**

Para ello, primero se crea la carpeta donde se guardarán los resultados
obtenidos del análisis de performance con VTune hecho desde la consola.
Accedemos a MobaXterm para Windows y ubicamos la carpeta recién creada.
:::

::: {#659b37a6-9d96-46c6-b368-056a03eb4752 .cell .markdown}
[alt text]{.image .placeholder original-image-src="cambio_carpeta.JPG"
original-image-title=""}
:::

::: {#8d7c8c17-2b60-412b-af84-508fe5ec70cb .cell .markdown}
Ahora se procede a descargar la carpeta **r000ps** la cual contiene los
resultados del análisis, con el siguiente comando: \"scp -r
devcloud:/home/u185959/computacion_paralela/CPAR_GPUs/r000ps .\"
:::

::: {#438bdc3a-ca4b-4f70-a5d9-3978d855e954 .cell .markdown}
[alt text]{.image .placeholder original-image-src="descarga_r000ps.JPG"
original-image-title=""}
:::

::: {#d7ed32cc-8e9b-43df-9247-0901c359d7ae .cell .markdown}
Se corrobora que la carpeta haya sido descargada en la carpeta creada de
la pc:
:::

::: {#fcacf05e-a78a-4200-9f0e-740f80c6725d .cell .markdown}
[alt text]{.image .placeholder original-image-src="descargado.JPG"
original-image-title=""}
:::

::: {#e1ad0b64-21ca-4328-a63f-f4a4a4b499db .cell .markdown}
En este punto, se ejecutará **VTune Offline**. Para ello se abre la
interfaz del programa y se selecciona el archivo **r000ps** para iniciar
el respectivo análisis sugerido por el software.
:::

::: {#109710cf-e100-406f-95d6-42b156beee97 .cell .markdown}
[alt text]{.image .placeholder original-image-src="VTune_ready.JPG"
original-image-title=""}
:::

::: {#8bf1d963-6d1e-44a2-86f9-c3088138a466 .cell .markdown}
Regresando al MobaXterm, se ingresará al nodo **gen11** para ejecutar el
análisis de hotspots:
:::

::: {#2f74b1c6-2c5c-4fc0-801c-0f2fe39bc4c8 .cell .markdown}
[alt text]{.image .placeholder original-image-src="connect_mobanodo.JPG"
original-image-title=""}
:::

::: {#63e61096-954e-4955-81a1-0c0f81d557ee .cell .markdown}
Ahora se realizará el análisis **gpu-hostpost** con el comando \"vtune
-collect gpu-hotspots \--
/home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/nbody\"
:::

::: {#5aaf0de4-29ad-41ff-b8b1-a7926bbec188 .cell .markdown}
[alt text]{.image .placeholder original-image-src="VTune_hostpots.JPG"
original-image-title=""}
:::

::: {#b13b5de3-5d4d-4557-ab44-b35d45cb56f1 .cell .markdown}
Con lo anterior se obtiene una carpeta llamada **r000gh** la cual se
descargará a la pc usando el comando \"scp -r
devcloud:/home/u185959/r000gh .\"
:::

::: {#66ea2ebd-dd8f-41ff-8012-6d0b789b0d97 .cell .markdown}
[alt text]{.image .placeholder original-image-src="copiando_nbody.JPG"
original-image-title=""}
:::

::: {#9e7ed9bd-a0c3-4603-a3b0-1375f0f7dae3 .cell .markdown}
Verificando que se haya descargado en la carpeta local:
:::

::: {#ce635a06-3295-44a1-8f56-d254ea83c2d4 .cell .markdown}
[alt text]{.image .placeholder original-image-src="carpeta_nbody.JPG"
original-image-title=""}
:::

::: {#0535a0db-3daf-4460-90db-37fb57fc1a26 .cell .markdown}
Ahora se usará el archivo **r000gh.vtune** para visualizar los
resultados del análisis de hotspots, con lo cual se obtiene el hostpot
de la aplicación:
:::

::: {#49b39f2d-c44b-4f91-8a8d-a7139ddda598 .cell .markdown}
[alt text]{.image .placeholder original-image-src="hotspot.JPG"
original-image-title=""}
:::

::: {#8a4ad26d-90dd-4663-96a5-ef4259e8aa4f .cell .markdown}
[alt text]{.image .placeholder original-image-src="memory_diagram.JPG"
original-image-title=""}
:::

::: {#f13cfb4b-63f4-4715-8149-3cbb868bfab6 .cell .markdown}
**Comentarios acerca del \"Memory Hierarchy Diagram\":** en la imagen se
visualiza el diagrama de bloques de jerarquía de un sistema compuesto de
un CPU y GPU integrado y cuya comunicación se realiza mediante la
memoria DRAM o también conocido como \"memoria del sistema\". Este
gráfico muestra también, el ancho de banda que alcanza la aplicación en
este GPU a través de la jerarquía de memoria que tiene el sistema. Por
ejemplo, el ancho de banda entre las memorias GTI y LLC es diferente
tanto como para lectura (lectura hacia la unidad de cómputo), igual a
26.9 MB/s, y escritura (desde el GPU hacia la memoria) igual a 68.4
MB/s, es decir el programa escribe más de lo que lee y sería un punto a
tomar en cuenta para mejoras futuras. La unidad de ejecución (execution
unit) indica con sus métricas el porcentaje de ocupación de 88.9%, lo
cual permite conocer que ha realizado tareas útiles en un 78.9% y tareas
no útiles un 18.3%.
:::

::: {#2f1fbc34-409b-4dab-b743-9f73df62cb19 .cell .markdown}
## 5. Realizar un análisis ***Roofline*** con Advisor \[4 puntos\] {#5-realizar-un-análisis-roofline-con-advisor-4-puntos}

-   Indicar los hotspots del programa
-   Proporcionar screenshot(s) de los resultados
-   Por cada screenshot, añadir una breve descripción
-   Indicar potenciales soluciones para optimizar la ejecución del
    programa
:::

::: {#3030c72b-ff28-4346-b3a0-1fd31bd82e8a .cell .markdown}
Primero, se accede a la ubicación del ejecutable que corresponde al
ejemplo de NBody escrito en SYCL:
:::

::: {#09045e88-87b4-43ed-b79f-b8fc026c8be9 .cell .code execution_count="25"}
``` python
cd ~/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/
```

::: {.output .stream .stdout}
    /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src
:::
:::

::: {#510d8c98-a3ba-4bb6-b9c7-17afa56a18be .cell .markdown}
Ahora, se procede a crear el archivo buil.sh
:::

::: {#198fbff2-48d7-4915-8c22-a21ada7017b2 .cell .code execution_count="26"}
``` python
%%writefile ~/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/build.sh
source /opt/intel/inteloneapi/setvars.sh > /dev/null 2>&1
mkdir build
cd build
cmake ..
make
```

::: {.output .stream .stdout}
    Writing /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/build.sh
:::
:::

::: {#03e93c5d-58d0-411f-9a04-f1355eded81f .cell .markdown}
Luego se crea otro archivo llamado run.sh
:::

::: {#2bddc497-4a55-4a22-b0fb-c3d3dd183988 .cell .code execution_count="27"}
``` python
%%writefile ~/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/run.sh
source /opt/intel/inteloneapi/setvars.sh > /dev/null 2>&1
cd build
make run
```

::: {.output .stream .stdout}
    Writing /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/run.sh
:::
:::

::: {#c9a565d9-7600-49e2-92e0-e664d5d65b39 .cell .markdown}
Ejecutando estos dos archivos:
:::

::: {#5cd94d31-7824-4702-80c8-924a9e452aac .cell .code execution_count="28"}
``` python
!qsub -l nodes=1:gpu:ppn=2 -d . build.sh
```

::: {.output .stream .stdout}
    2255146.v-qsvr-1.aidevcloud
:::
:::

::: {#b866632a-d947-4452-ae02-4305b30d8b43 .cell .code execution_count="29"}
``` python
!qsub -l nodes=1:gpu:ppn=2 -d . run.sh
```

::: {.output .stream .stdout}
    2255147.v-qsvr-1.aidevcloud
:::
:::

::: {#d8ea9934-c29a-4780-a2a8-228d1f78004b .cell .markdown}
Con ello, se obtiene el ejecutable **NBody** para usarlo en el software
Advisor. En esta ubicación ejecutamos el siguiente comando:
:::

::: {#8d303464-fb80-4438-9fff-2381d6084d85 .cell .code execution_count="30"}
``` python
!advisor --collect=roofline --project-dir=./advi_results -- ~/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/nbody
```

::: {.output .stream .stdout}
    advisor: Warning: The Roofline is a special batch mode of data collection. It runs two analyses one by one. There are Survey Analysis and Trip Counts Analysis with FLOP respectively.
    advisor: Starting command line: advisor --collect survey --project-dir ./advi_results -- /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/nbody
    Intel(R) Advisor Command Line Tool
    Copyright (C) 2009-2023 Intel Corporation. All rights reserved.
    advisor: Collection started. To stop the collection, either press CTRL-C or enter from another console window: advisor -r /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/advi_results/e000/hs000 -command stop.
    ===============================
     Initialize Gravity Simulation
     nPart = 16000; nSteps = 10; dt = 0.1
    ------------------------------------------------
     s       dt      kenergy     time (s)    GFLOPS      
    ------------------------------------------------
     1       0.1     26.405      0.44998     16.499      
     2       0.2     313.77      0.026332    281.95      
     3       0.3     926.56      0.017184    432.05      
     4       0.4     1866.4      0.015776    470.61      
     5       0.5     3135.6      0.015988    464.38      
     6       0.6     4737.6      0.015787    470.28      
     7       0.7     6676.6      0.016815    441.53      
     8       0.8     8957.7      0.016183    458.76      
     9       0.9     11587       0.015997    464.11      
     10      1       14572       0.01595     465.49      

    # Total Time (s)     : 0.6062
    # Average Performance : 458.4 +- 13.172
    ===============================
    advisor: Collection stopped.
    advisor: Opening result 21 % Resolving information for `libstdc++.so.6'        
    advisor: Warning: Cannot locate debugging information for file `/lib64/ld-linux-x86-64.so.2'.
    advisor: Opening result 21 % Resolving information for `nbody'                 
    advisor: Warning: Cannot locate debugging information for file `/glob/development-tools/versions/oneapi/2023.0.1/oneapi/advisor/2023.0.0/lib64/runtime/libittnotify_collector.so'.
    advisor: Warning: Cannot locate debugging information for file `/lib/x86_64-linux-gnu/libstdc++.so.6'.
    advisor: Opening result 21 % Resolving information for `libclang_compiler.so.20
    advisor: Warning: Cannot locate debugging information for file `/glob/development-tools/versions/oneapi/2023.0.1/oneapi/advisor/2023.0.0/lib64/libtpsstool.so'.
    advisor: Opening result 21 % Resolving information for `libc.so.6'             
    advisor: Warning: Cannot locate debugging information for file `/lib/x86_64-linux-gnu/libc.so.6'.
    advisor: Opening result 22 % Resolving information for `libdl.so.2'            
    advisor: Warning: Cannot locate debugging information for file `/lib/x86_64-linux-gnu/libdl.so.2'.
    advisor: Opening result 22 % Resolving information for `libpthread.so.0'       
    advisor: Warning: Cannot locate debugging information for file `/lib/x86_64-linux-gnu/libpthread.so.0'.
    advisor: Opening result 99 % done                                              
    advisor: Preparing frequently used data  1 % done                              
    advisor: Preparing frequently used data 100 % done                             
    advisor: Warning: Some target modules do not contain debug information 
    advisor: Warning: Your application might be underperforming 
    advisor: Warning: Application with offload directives may require a GPU-specific analysis 

    Program Elapsed Time: 6.25s

    CPU Time: 6.25s
    Time in 3 Vectorized Loops: 1.94s

    advisor: Starting command line: advisor --collect tripcounts --project-dir ./advi_results --flop --no-trip-counts -- /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/nbody
    Intel(R) Advisor Command Line Tool
    Copyright (C) 2009-2023 Intel Corporation. All rights reserved.
    advisor: Opening result 25 % done                                              
    advisor: Preparing frequently used data  1 % done                              
    advisor: Preparing frequently used data 100 % done                             
    advisor: Collection started. To stop the collection, either press CTRL-C or enter from another console window: advisor -r /home/u185959/computacion_paralela/CPAR_GPUs/oneAPI-samples/DirectProgramming/C++SYCL/N-BodyMethods/Nbody/build/src/advi_results/e000/trc000 -command stop.
    ===============================
     Initialize Gravity Simulation
     nPart = 16000; nSteps = 10; dt = 0.1
    ------------------------------------------------
     s       dt      kenergy     time (s)    GFLOPS      
    ------------------------------------------------
     1       0.1     26.405      26.9        0.276       
     2       0.2     313.77      0.065468    113.4       
     3       0.3     926.56      0.0337      220.31      
     4       0.4     1866.4      0.024815    299.18      
     5       0.5     3135.6      0.026541    279.73      
     6       0.6     4737.6      0.024957    297.48      
     7       0.7     6676.6      0.020094    369.47      
     8       0.8     8957.7      0.020192    367.68      
     9       0.9     11587       0.019996    371.28      
     10      1       14572       0.020601    360.39      

    # Total Time (s)     : 27.18
    # Average Performance : 320.69 +- 51.816
    ===============================
    advisor: Opening result 100 % done                                             
    advisor: Preparing frequently used data  1 % done                              
    advisor: Preparing frequently used data 100 % done                             
    advisor: Warning: Some target modules do not contain debug information 
    advisor: Warning: Your application might be underperforming 
    advisor: Warning: Application with offload directives may require a GPU-specific analysis 

    Program Elapsed Time: 6.25s

    CPU Time: 6.25s
    Time in 3 Vectorized Loops: 1.94s
    GFLOPS: 11.06
    GINTOPS: 0.05
:::
:::

::: {#2700d2ff-07c4-4a59-962f-9cac47597818 .cell .markdown}
Con este procedimiento se ha creado la carpeta \"advi_results\" donde se
han guardado todos los resultados del Roofline del nodo que se está
usando. Así, se procede a copiar a la pc local mediante MobaXterm:
:::

::: {#f232e767-df4a-4391-90f5-17fbc0dd0af3 .cell .markdown}
[alt text]{.image .placeholder
original-image-src="copy_carpeta_advisor.JPG" original-image-title=""}
:::

::: {#5fe437dc-8cd6-4e51-90b2-6564ad27bbd4 .cell .markdown}
Verificando que se haya copiado correctamente en la carpeta de destino
local:
:::

::: {#86ad9355-2a2b-402b-bc95-9e7bd902a4f3 .cell .markdown}
[alt text]{.image .placeholder
original-image-src="carpeta_advisor_results.JPG"
original-image-title=""}
:::

::: {#779efef0-2172-48e4-84b7-9972b0396ec6 .cell .markdown}
Ahora se procede a abrir el software **Advisor** para ejecutar el
archivo obtenido en la carpeta \"advi_results\". Con ello se obtienen
los resultados del análisis roofline que se observan en la siguiente
figura:
:::

::: {#ec6f7128-2238-4fe5-9620-900e7af7a4b2 .cell .markdown}
[alt text]{.image .placeholder original-image-src="roofline_dann2.JPG"
original-image-title=""}
:::

::: {#b17999c3-4b46-4bf3-9909-caa482c3f561 .cell .markdown}
[alt text]{.image .placeholder original-image-src="roofline_dann.JPG"
original-image-title=""}
:::

::: {#d4e1cfd4-d162-436d-b665-6b193b74816c .cell .markdown}
De la imagen obtenida al realizar el **roofline** en Advisor para el
algoritmo **NBody** se puede observar que hay una sección que tiene
potencial de incrementar su velocidad en el algoritmo, por ende no está
explotando el potencial del sistema sobre el cual se ha ejecutado. Una
posible mejora sería aumentando el número de operaciones para lograr un
mayor rendimiento.
:::

::: {#c84e9043-33a1-4b4c-8d88-926bc7a9afee .cell .code}
``` python
```
:::
