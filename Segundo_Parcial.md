1. ***Introducción a la sincronización***
  - Sincronizar implica codificar un protocolo de programación, con el objetivo de compartir recursos.
  - Race condition se da cuando 2 o más procesos sin algún protocol para compartir recursos están compitiendo por ese recurso. Se le dice race condition porque es una carrera para ver quien usa finalmente el recurso.
  - Sección crítica: **Fragmento de código** de un proceso, en el cuál se utiliza un recurso computacional compartido. **Debe cumplirse la exclusión mutua y progreso**
  - Exclusión mutua: Capacidad que permite que **sólo un proceso** esté ejecutando una sección crítica la cual comparte un recurso con otros procesos. Dado que si un proceso está en la SC y otro quiere entrar. Este último debe esperar a que el primero termine.
  - Progreso: Si ningún proceso que pertenece a un conjunto de procesos está en la sección crítica, y uno de esos procesos quiere entrar a la sección crítica debe poder hacerlo.
  - Espera limitada: Si un proceso desea acceder a su SC, debe poder hacerlo dentro de un tiempo razonable.
2. ***Sincronización de procesos***
  - Hay varias herramientas que ayudan para compartir recursos, herramientas como:
    - Software
      - Código el usuario
      - Semáforos
      - Monitores
    - Hardware
      - Test-and-set
      - Swap
  - Mejor algoritmo para 2 procesos:
    ```pseudo
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
    ```
  - El algoritmo del repostero garantiza que teniendo n procesos, esos n procesos van a compartir eficientemente algún o algunos recursos.
    ```pseudo
    status[i]:=true;
    turno[i]:=max(turno[0], turno[1], ..., turno[n-1]) + 1; // Asigna el siguiente turno
    status[i]:=false;
    for j:=0 to n-1
     do begin
     while status[i] do no-op;
     while turno[j] != 0 and turno[j] < turno[i] do no-op;
    end
    ```
  - Pasos para verificar que el algoritmo de sincronización funciona correctamente:
    1. ¿Qué pasa si P1 llega primero que P2 a la sección crítica?
    2. ¿Qué pasa si P2 llega primero que P1 a la sección crítica?
    3. ¿Qué pasa si ambos procesos intentan acceder a la sección crítica al mismo tiempo?
3. ***Introducción a semáforos***
  - Esta herramienta pretende solucionar los problemas de:
    - La dificultad de programar soluciones
    - La ineficiencia
  - Ventajas:
    - Los semáforos permiten sincronizar con facilidad a n procesos.
    - Están precodificados. Su operación en sí misma está libre de errores.
    - Son eficientes. Debido a que no se necesita de un bucle en su operación
  - Los semáforos son variables especiales el cual contiene valores enteros, inventados por Djikstra.
  - Se basa en el uso de los métodos atómicos P y V, para esperar o accionar las acciones.
  - Hay 2 tipos de semáforos: Binarios y Generales.
    - Los semáforos binarios pueden tomar únicamente los valores 0 y 1.
    - Los semáforos generales pueden tomar valores enteros positivos y negativos.
  - Uso correcto de semáforos:
    ```pseudo
    Var S: Semáforo_Binario;
    InitSemaphore(S, 1);
    Proceso P1;
    BEGIN
      P(S)
      //Sección crítica
      V(S)
    END
    ```
  - Cuando un semáforo está en valores negativos indica que ya no hay recursos disponibles, de manera que detiene el proceso hasta que haya nuevos.
  - Algoritmo productor-consumidor con semáforos:
    ```pseudo
    int saca, agrega, dato, dato1, buff[100];
    Var ocupados, disponibles: semaforo_gral;
    Var buffer: semaforo_binario;
    Process P1()
    begin
      while true do
        produce;
        P(disponibles);
        P(buffer);
        buff[agrega] = dato;
        agrega = (agrega + 1) % dato;
        V(buffer);
        V(ocupados);
      end
    end
    Process P2()
    begin
      while true do
        produce;
        P(ocupados);
        P(buffer);
        dato1 = buff[saca];
        saca = (saca + 1) % dato;
        print(dato1);
        V(buffer);
        V(disponibles);
      end
    end
    ```
4. ***Introducción a monitores***
  - Los monitores son tipos de datos abstractos.
  - Las variables del monitor sólo pueden ser accesadas por los procedimientos del mismo.
  - Sólo puede haber una función ejecutándose en el monitor, garantizando la exclusión mútua.
  - Ejemplo de código de un monitor:
    ```pseudo
    Monitor x();
    rutina_1(){

    }
    rutina_2(){

    }
    end_monitor;
    ```
  - Hay 3 posibles clases de filas en un monitor: De entrada, de variables de condición, especial.
    1. Fila de entrada: Se bloquean los procesos que hacen una invocación a una rutina del monitor pero que no pueden entrar debido a que hay otro proceso.
    2. Variables de condición:
      - Son variables protegidas que sólo soportan los métodos wait y signal.
      - Estas son declaradas y utilizadas dentro del monitor.
      - A diferencia de un semáforo no tiene valor y sólo sirve para movilizar alguna fila, además que no se inicializan.
