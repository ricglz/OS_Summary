1. ***Introducción a la sincronización***
  - Sincronizar implica codificar un protocolo de programación, con el objetivo de compartir recursos.
  - Race condition se da cuando 2 o más procesos sin algún protocol para compartir recursos están compitiendo por ese recurso. Se le dice race condition porque es una carrera para ver quien usa finalmente el recurso.
  - Sección crítica: **Fragmento de código** de un proceso, en el cuál se utiliza un recurso computacional compartido. **Debe cumplirse la exclusión mutua y progreso**
  - Exclusión mutua: Capacidad que permite que **sólo un proceso** esté ejecutando una sección crítica la cual comparte un recurso con otros procesos. Dado que si un proceso está en la SC y otro quiere entrar. Este último debe esperar a que el primero termine.
  - Progreso: Si ningún proceso que pertenece a un conjunto de procesos está en la sección crítica, y uno de esos procesos quiere entrar a la sección crítica debe poder hacerlo.
  - Espera limitada: Si un proceso desea acceder a su SC, debe poder hacerlo dentro de un tiempo razonable.
2. ***Sincronización de procesos***
  - Herramientas de sincronización:
    - Software
      - Código el usuario
      - Semáforos
      - Monitores
    - Hardware
      - Test-and-set
      - Swap
  - Mejor algoritmo para 2 procesos:
    `
    // Proceso 0
    Begin
    repeat
      flag[0]:=true
      turn:=1
      while(flag[1] and turn==1)
        do no-op;
      counter:=counter + 1;
      flag[0]:=false
    until false;
    end
    //Proceso 1
    Begin
    repeat
      flag[0]:=true
      turn:=1
      while(flag[1] and turn==1)
        do no-op;
      counter:=counter + 1;
      flag[0]:=false
    until false;
    end
    `
