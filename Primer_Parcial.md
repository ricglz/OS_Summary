1. Introducción
 - Un sistema operativo es aquel que controla los dispositivos y asigna los recursos de una terminal.
2. Procesos
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