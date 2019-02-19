1. ***Introducción***
 - Un sistema operativo es aquel que controla los dispositivos y asigna los recursos de una terminal.
2. ***Procesos***
  - Thread: Es un contexto único de ejecución
  - Proceso: Programa de ejecución, puede llegar a contener varios
    - Threads
    - Registros
    - Memoria
    - Entre otros
  - PCB (Process Control Block): Provee de información sobre procesos.
  - Espacio de dirección: Donde se ejecutan los programas.
  - Modo dual: Permite cambiar de modo usuario a modo privilegiado.
  - Modo privilegiado: Modo en el que se pueden llamar funciones del kernel o SO.
  - Kernel: Núcleo del SO (procesos).
  - Arquitectura: Hay arquitecturas monolíticas, por capas y de cliente/servidor
  - Diagrama de estados: Son los estados en los que se encuentran los procesos. Los 3 más comunes son: Listo(Aquellos programas que pueden ser ejecutados), corriendo y bloqueado(programas que está esperando una respuesta de I/O).
  - Los procesos hijos en UNIX se pueden crear con fork + execve.
    - Si un hijo ejecuta fork, regresa un número mayor a cero. Si un padre ejecuta un fork puede regresar 0 si los hijos fueron creados o -1 si hubo algún error en el proceso.
3. ***Admininistración de procesos***
  - Round Robin: Es algoritmo en que cada proceso va uno tras uno a partir como vaya llegando, pero el tiempo de cada proceso es limitado por el Quantum.
  - SJF/SRT: Según el tamaño de ráfaga (Tiempo)
  - FIFO: Sin expulsar, uno por uno.
  - Priority: Dependiendo de la prioridad. Cualquier algoritmo de prioridad recae en starvation.
  - Non preemptive: No se puede expulsar el proceso del CPU.
4. ***Métricas de proceso***
  - Throughput = procesos terminados / tiempo
  - Turnaround (tiempo de retorno) = tFinal - tInicial = tEspera + tCPU
  - Waiting time: Todo tiempo en el que el CPU no esté en ejecución, comúnmente no se toma en cuenta cuándo está en bloqueado por facilidad, pero puede variar.
  - Response time: Tiempo en el que se visualiza el primer cambio del programa.
  - Tiempo de usuario: CPU en modo usuario.
  - Tiempo de sistema: CPU en modo privilegiado.
  - Tiempo en CPU = tUsuario + tSistema