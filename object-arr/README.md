# Los métodos que confundo u olvido

## arr to str, str to arr

* .join (unirse) .split (dividir)

## por el nombre

* .slice (tajada o corte) .splice (empalme) .split (dividir) (tambien me para con Math.ceil(); pienso 'es "ceil" o "ceil" es de esos métodos que siempre confundo')

## clonar arr

var arrClone = arr.slice(x) //donde x el el indice desde el que inicia la clonación 
slice en castellano es como cortar o rebanar (rebanada de pastel).

## empalme arr: esto sieve para agregar o eliminar elementos de un arreglo

```javascript
array.splice(start, deleteCount, item1, item2, ...);

/*            
start: Índice desde el cual se realizarán las modificaciones.

deleteCount: Número de elementos a eliminar desde start. Si es 0, no se eliminará ningún elemento.

item1, item2, ...: Elementos a agregar en el array a partir de la posición start.
*/
```

# Olvido su función o diferencias

## En Objetos probar si existe la propiedad con <consulta-directa>, <in>, o con <hasOwnProperty>
### ¿qué hace <in> y que problemas tiene?


* La consulta directa **propiedad.objeto** siempre retornara algo aunque la propiedad no exista.

* Problemas:

    * En general funciona bien. Uno de los problemas es cuando esa propiedad es heredada lo que puede causar confusión

    * Otro problema es que la propiedad si exista pero por algún motivo su valor es **undefined**


* El operador **in** prueba si es que la propiedad está en el objeto devolviendo true o false:
    'propiedad' in objeto

    * la ventaja del operador **in** respecto a la consulta directa es que retoranará **false** en vez de **undefined** si es que la propiedad no existe.

    * Una de las cosas que se me suele olvidar es que el nombre de la propiedad tiene que ser escrito ***entre comillas*** si es un string.

    * las comillas solo se ***omiten*** cuando la key de la propiedad es un número o en el caso de que se utilize una variable que almacene el nombre de la propiedad.

* Problemas:

    * Al igual que con la consulta directa **in** no distinguirá entre una propiedad del objeto y otra heredada entonces ***'constructor' in obj*** siempre retornara **true** ya que constructor es una propiedad (***método***) del prototipo **Object.prototype**


* El método **hasOwnProperty()** solo consultara por propiedad ***propias del objeto*** (no heredadas)


* en general una ***consulta-directa*** debería ser suficiente
* ocupar el método **hasOwnProperty()** es más seguro y se ve más profesional
* Al igual que con el operador **in** con el método **.hasOwnProperty('argumento')** hay que ingresar los strs entre comillas