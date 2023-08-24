### Los métodos que confundo u olvido

1) .join (unirse) .split (dividir)
2) .slice (tajada o corte) .splice (empalme) .split (dividir)

## clonar arr

var arrClone = arr.slice(x) //donde x el el indice desde el que inicia la clonación 
slice en castellano es como cortar o rebanar (rebanada de pastel).

## empalme arr
# esto sieve para agregar o eliminar elementos de un arreglo

array.splice(start, deleteCount, item1, item2, ...)

start: Índice desde el cual se realizarán las modificaciones.

deleteCount: Número de elementos a eliminar desde start. Si es 0, no se eliminará ningún elemento.

item1, item2, ...: Elementos a agregar en el array a partir de la posición start.