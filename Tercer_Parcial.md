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
