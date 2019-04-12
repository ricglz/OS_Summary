1. ***Introducción a la administración de memoria***
  - La administración de memoria se encarga de la optimización de esta, maximando cantidad de espacio ocupado.
  - Las asignaciones de memoria en un SO, se puede realizar de distintas maneras:
    * Con respecto a la memoria real:
      * Particiones fijas o estáticas.
      * Particiones dinámicas o variables.
    * Con respecto a la memoria virtual:
      * Segmentación
      * Paginación
      * Memoria virtual
  - Tipos de almacenamiento:
    * Almacenamiento contiguo: El programa y los datos relacionados se cargan en memoria como un todo.
    * Almacenamiento disperso: El programa y sus datos se almacenan fraccionalmente en la memoria.
  - Cómo está organizada la memoria (**Organización de memoria**)
    * Esquemas de alojamiento contiguo: Con el uso de particiones fijas o variables
    * Esquemas de alojamiento disperso: Usando paginación, segmentación o una combinación de ambas.
  - Políticas de administración de memoria
    * **Fetch**, o cargar en español, es leer de la memoria secundaria para traerla a la memoria principal.
    * **Colocación**, el decidir dónde voy a colocar en memoria el programa o dato.
    * **Remplazo**, decidir que quitar de memoria si acaso todo llegase a estar ocupado
  - Requerimientos:
    * **Relocalización**: Convertir una dirección lógica o relativa, en una física o absoluta.
      * El MMU (**Memory-Management Unit**) es el que se encarga de "traducir" las direcciones lógicas en físicas.
    * Protección: Es asegurar que cada proceso esté protegido de interferencias causadas por otros procesos.
    * Compartición: Permitir que varios procesos y/o usuarios acceden la misma porción a la memoria principal.
  - Overlay: Mantener en memoria sólo aquellas instrucciones y datos que se necesitan en un momento dado de la ejecución
  - Estrategias de colocación:
    * **First fit**, se coloca en el primer bloque de memoria que pueda contener el proceso.
    * **Best fit**, se colocal en el bloque más pequeño que pueda contenerlo.
    * **Worst fit**, se colocal en el bloque más grand que pueda contenerlo.
  - **Tipos de fragmentación**:
    * Externa: La cantidad de espacio libre no contigua (junta) de la RAM.
    * Interna: El espacio no utilizado de un bloque de memoria. Porque el bloque es de mayor tamaño que el del proceso.
  - **Soluciones para fragmentación externa**:
    * Compactación: Recorre físicamente la memoria, con el objetivo de colocar junta toda la memoria libre en un sólo bloque. **Nota** Esto sólo es posible si se tiene relocalización dinámica.
    * Aglutinamiento: Juntar 2 bloques libres de memoria en uno sólo.
2. ***Paginación***
  - Uno de los problemas de administrar la memoria tomando en cuenta únicamente la memoria física, es que no permite que los procesos sean más grandes que la memoria real. Por ello surgió la memoria virtual.
  - En paginación cada proceso se divide en "páginas" o bloques de igual tamaño. Este tamaño siempre es una potencia de 2.
  - La memoria física se divide en bloques de tamaño fijo llamados marcos de página.
  - Las páginas de los procesos son cargados en los marcos de páginas.
  - Cuando una página se necesita puede llegar a haber 3 resultados
    1. Que ya esté en RAM
    2. No está en memoria, por lo que será necesario traerla de la memoria secundaria.
    3. Referencia invalida, debido a que intenta hacer una referencia a una página que no es del proceso.
  - Una dirección virtual cuando se usa paginación se expresa como **_v=(p, d)_**
    - p es el número de página a la que se hace referencia.
    - Mientras que d es el desplazamiento.
  - Para obtener la dirección física a partir de la dirección virtual, se debe realizar lo siguiente
    1. Obtener los valores de p y d
      - Si la dirección virtual está en formato decimal. p = v / tam_pagina y d = v % tam_pagina
      - Si está en formato binario. Tenido que el tam_pagina = 2 ^ n, los primeros n dígitos de derecha a izquierda es d, los restantes son p.
    2. Verifcar que d sea menor que el tamaño de página. Si no lo es entonces hay un page overflow.
    3. Obtener el marco de página
    4. Calcular la dirección real usando el marco de página y d
      - Si la dirección virtual está en formato decimal. dir_real = marco_de_pagina * tam_pagina + d
      - Si está en formato bianrio. Se concatena el mp (marco de página) con d, de manera que si mp=111 y d=0000, dir_real=1110000
  - Las tablas de páginas son mantenidas en memoria principal.
3. ***Segmentación***
  - Cada proceso se divide en "secciones" llamados segmentos, pudiendo ser de diferente tamaño cada uno.
  - La dirección virtual cuando se usa segmentación se expresa como **_v=(s, d)_**
    - s siendo el número de segmento
    - d el desplazamiento
  - Estructura de la tabla de segmentos
    - Bit de residencia
    - Dirección en memoria secundaria
    - Tamaño del segmento
    - Bits de protección
    - Dirección base del segmento en memoria real
  - Bits de protección utilizados: R (Read), W (Write), E (Execute), A (Append)
    - Cualquier combinación de estas es posible, a excepción que no se incluya R, pero que sí se permita W.
  - Para obtener la dirección física a partir de la dirección virtual, se debe realizar lo siguiente
    1. Obtener los valores de s y d. Para esto se debe usar un mapa del proceso, para ver cómo están divididos los segmentos y en qué direcciones.
    2. Verificar que s está o no en memoria, sino es así sucede un Segmentation Fault.
    3. Tras haber encontrado el segmento, verificar que d sea menor que la longitud del segmento, sino es así sucede un segmentation overflow
    4. Obtener la base
    5. Obtener la dirección real. Para esto se suma la base + d
  - Se puede combinar segmentación con paginación.
    - En este caso **_v=(s, p, d)_**
      - s sería el segmento donde se encuentran las páginas
      - p sería la página que se encuentra en el segmento
      - d sería el desplazamiento
4. ***Administración de Memoria Virtual II***
  - Los procesos compiten por todos los marcos de página
  - Hay diferentes asignacios para estos marcos de página:
    - Asignación máxima, a cada proceso se le asigna uno máximo.
    - Asignación equitativa, todos los procesos tienen la misma cantidad de marcos.
    - Asignación proporcional
      - Se le asigna marcos de acuerdo al tamaño en KB de los procesos.
      - marcos =  tamaño_proceso / suma_de_tamaños_de_procesos * max_cantidad_de_marcos
    - Asignación por prioridades
      - Se le asigna marcos de acuerdo a la prioridad
      - Si el número de prioridad es mayor, se tiene mayor prioridad. marcos = prioridad / suma_de_prioridades * max_cantidad_de_marcos. **Nota** la prioridad mínima debe ser 1.
      - Si el número de prioridad es mayor, se tiene mayor prioridad. marcos = (max_prioridad - prioridad + 1) / suma_de_prioridades * max_cantidad_de_marcos.
  - Tipos de reemplazo
    - Global. Escoger un marco de página de todos los marcos que hay en todos los procesos.
    - Local. Escoger un marco de página de todos los marcos que hay en un sólo proceso.
  - Thrashing: Cuando un proceso invierte más tiempo paginando, que ejecutando instrucciones de los procesos.
  - Equemas diseñados para evitar "thrashing"
    - Working Set: Teniendo un tiempo X y un número N, haces un conjunto de los últimas N referencias desde el tiempo X.
    - Modelo de Page Fault Frecuency
