# statement es lo mismo que sentencias.

* Los statement hacen algo.

## keywords loop

* break vs continue.
    * estos solo se pueden ocupar dentro de bucles.

## operaciones en objetos

* delete (delit) 
    se ocupa delante de una propiedad que se quiera eliminar.
*
*

## this


* this es autorreferencial que se puede aplicar en cada objeto
* Cuando se llama dentro de un objeto, se refiere a ese mismo objeto.
* **this** puede usarse para acceder a otras claves en el mismo objeto, y es especialmente útil en métodos:

```javascript
const usuario = {
    username: 'juan.perez',
    password: 'loremipsumpwd123',
    lovesJavascript: true,
    favoriteNumber: 42,
    decirHola: function(){
        console.log( this.username + ' manda saludos!');
    }
};

usuario.decirHola(); // 'juan.perez manda saludos!'
```

###### `this` a veces puede ser uno de los temas más difíciles en Javascript.

* Cuando ejecutamos código en el contexto global (afuera de cualquier función). En este caso `this` hace referencia al objeto `global`, en el caso del browser hace referencia a `window`.

``` javascript
// En el browser esto es verdad:
> console.log(this === window);
< true

> this.a = 37;

> console.log(window.a);
< 37
```

### En el contexto de una función

Cuando estamos dentro de una función, el valor de `this` va a depender de **cómo sea invocada la función**.

``` javascript
> function f1(){
    return this;
  }

> f1() === window;
< true

> window.fi() === window;
< true
```

function f1(){
    return this;
  }

f1() === window;


window.fi() === window;


***En este ejemplo la función es invocada por el objeto global por lo tanto this hará referencia a `window`.***



### Como método de un objeto

* `this` dentro de una función que es un método de un objeto, hace referencia al objeto sobre el cual se llamó el método:

``` javascript
> var o = {
    prop: 37,
    f: function() {
      return this.prop;
    }
  };

> console.log(o.f());
< 37
// this hace referencia a `o`
```

***En este caso, no depende donde hayamos definido la función, lo único que importa es que la función haya sido invocada como método de un objeto*** Por ejemplo, si definimos la función afuera:

``` javascript
> var o = {prop: 37};

// declaramos la función
> function loguea() {
    return this.prop;
  }

//agregamos la función como método del objeto `o`
> o.f = loguea;

> console.log(o.f());
< 37
// el resultado es le mismo!
```

###### Hay que tener cuidado con `this`, ya que pueden aparecer casos donde es contra intuitivo

``` javascript
> var obj = {
    nombre: 'Objeto',
    log: function(){
      this.nombre = 'Cambiado'; // this se refiere a este objeto, a `obj`
      console.log(this)  // obj

      var cambia = function( str ){ //OJO ACÁ A LA FUNCIÓN CAMBIA

        this.nombre = str;  // Uno esperaria que this sea `obj`
      }

      cambia('Hoola!!');
      console.log(this);
    }
  }
```

* Si ejecutamos el código de arriba, vamos a notar que después de ejecutar el código, la propiedad `nombre` de `obj`
contiene el valor `Cambiado` y no `'Hoola!!'`

* **this** dentro de la **función cambia** NO hace referencia a **obj**, si no que hace referencia al **objeto global**.
* la **f cambia** no es metodo de **obj**. No es posible acceder a **f cambia** mediante ***obj.cambia*** (no es metodo).

###### como consecuencia de lo anterior:

* dentro del **objeto global** se podrá encontrar la variable **nombre**, con el valor **'Hoola!!'** que seteamos con la **f cambia**

###### **No importa** en donde estuvo declarada la función, si no **cómo la invocamos**.

###### es dificil saber el valor que va a tomar ***this*** hasta el momento de ejecución de una función. Porque depende fuertemente de cómo haya sido ejecutada.

* Para resolver este tipo de problemas existe un patrón muy común, y ***se basa en guardar la referencia al objeto que está en `this`*** antes de entrar a una función donde no sé a ciencia cierta que valor puede tomar `this`:

```javascript
var obj = {
  nombre: 'Objeto',
  log   : function(){
    this.nombre = 'Cambiado'; // this se refiere a este objeto, a `obj`
    console.log(this); // obj

    var that = this; // ***  Guardo la referencia a this ***

    var cambia = function( str ){
      that.nombre = str;  // Uso la referencia dentro de esta funcion
    }

    cambia('Hoola!!');
    console.log(this);
  }
}
```

* `that` (u otro nombre) va a apuntar al objeto (`obj`). Ahora si, podemos usar `that` en vez de `this` y estar seguros qué es lo que va a tener adentro.