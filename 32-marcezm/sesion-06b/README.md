# sesion-06b
Viernes 25 de Septiembre

## apuntes sesión

### Bibliotecas e instrucciones `#include`

```cpp
#include <stdio.h>
#include "pico/stdlib.h"
```
- `#include` permite incorporar archivos que contienen declaraciones de funciones y otras herramientas necesarias.
- `#include <stdio.h>`: incorpora la biblioteca estándar de entrada y salida de C. Permite utilizar funciones como `printf()`.
- `#include "pico/stdlib.h"`: incorpora el archivo de la biblioteca estándar de Raspberry Pi Pico.

***Diferencia entre `<>` y `""`:***

- Con `<>` se buscan normalmente bibliotecas del sistema o rutas de inclusión configuradas por el compilador.
- Con `""` se busca primero en las ubicaciones locales correspondientes al archivo y después en las demás rutas configuradas.

En este caso, `pico/stdlib.h` corresponde a una ruta dentro de la estructura de archivos de la biblioteca Pico.

### Función `main()`

```cpp
int main() {
    stdio_init_all();

    while (true) {
        printf("Hello, Wokwi!\n");
        sleep_ms(250);
    }
}
```
- `int main()`: es la función principal del programa. En un programa convencional de C/C++, la ejecución comienza desde esta función.
- `int`: indica que la función devuelve un número entero.
- `stdio_init_all();`: inicializa los canales de entrada y salida estándar configurados para el entorno de Pico.
- `while (true)`: repite las instrucciones que están dentro de las llaves indefinidamente.
- `printf("Hello, Wokwi!\n");`: muestra el mensaje `Hello, Wokwi!`.
- `\n`: agrega un salto de línea.
- `sleep_ms(250);`: pausa la ejecución durante 250 milisegundos.

En este ejemplo, el mensaje aparece aproximadamente cuatro veces por segundo.

*Normalmente `return 0;` indica que la ejecución terminó correctamente. Los valores distintos de cero suelen utilizarse para indicar errores.

Sin embargo, en este ejemplo el programa permanece dentro del `while (true)`, por lo que no llega al final de la función.

#### ¿Qué significa que todo esté dentro de `main()`?
Generalmente `main()` es el punto de entrada. Las funciones que definimos por separado deben ser llamadas para que se ejecuten.

Podemos definir una función fuera de `main()` y después llamarla desde dentro de esta función principal.

### Ejemplo de una función propia

```cpp
int prueba() {
    int x = 3;
    int y = 6;
    int resultado = x * y;

    return resultado;
}
```
- `int`: indica que la función devuelve un número entero.
- `prueba`: nombre de la función.
- `()`: paréntesis donde podemos declarar parámetros.
- `int x = 3;`: crea una variable entera con valor 3.
- `int y = 6;`: crea una variable entera con valor 6.
- `int resultado = x * y;`: multiplica ambos valores y guarda el resultado.
- `return resultado;`: devuelve el resultado de la operación.

### ¿Cómo llamamos a la función?
Para ejecutar la función, escribimos su nombre seguido de paréntesis:
```cpp
prueba();
```

Si queremos mostrar el resultado en la consola, podemos utilizar `printf()`.
```cpp
printf("%d\n", prueba());
```

Resultado:
```text
18
```
**Importante:* este ejemplo no convierte un `int` en un `char`. Lo que hace es mostrar el entero que devuelve `prueba()` utilizando un especificador de formato.*

### ¿Qué significa `%d`?
`%d` es un especificador de formato utilizado por `printf()` para indicar que en esa posición se mostrará un número entero decimal.

```cpp
int edad = 20;

printf("Edad: %d\n", edad);
```

**Resultado:**
```text
Edad: 20
```
- `%`: indica que comienza un especificador de formato.
- `d`: indica un entero decimal.
- `\n`: agrega un salto de línea.

**Otros especificadores comunes:**
- `%d`: entero decimal.
- `%f`: número de punto flotante, como un `float`.
- `%c`: carácter individual.

#### Placeholder
Un placeholder es un marcador de posición que reserva un espacio para colocar un valor.

En el ejemplo anterior, `%d` funciona como marcador de posición para el valor de `edad`. Cuando se ejecuta `printf()`, ese marcador se reemplaza por el número correspondiente.

---

### Función `prueba()`
En el segundo ejemplo se incorpora la función propia y se llama desde `main()`.

```cpp
#include <stdio.h>
#include "pico/stdlib.h"

// Mi propia función
int prueba() {
    int x = 3;
    int y = 6;
    int resultado = x * y;

    return resultado;
}

// Función principal
int main() {
    stdio_init_all();

    while (true) {
        printf("%d\n", prueba());
        sleep_ms(250);
    }
}
```

realiza los siguientes pasos:
1. Incorpora las bibliotecas necesarias.
2. Define la función `prueba()`, que multiplica 3 por 6.
3. Inicializa la entrada y salida estándar.
4. Llama a `prueba()` desde `main()`.
5. Muestra el resultado mediante `printf()`.
6. Repite el proceso cada 250 milisegundos.

El resultado que veremos en la consola será `18`, repetido aproximadamente cuatro veces por segundo.

---

## 4. Charla en clases
- **Programar sin computadores:** practicar escribiendo código en papel permite trabajar la lógica de manera mecánica y comprender los pasos del programa sin depender del computador.
- **No casarse con las ideas iniciales:** no todo funciona a la primera, es importante probar otras alternativas y presentar una solución, aunque no sea exactamente el plan A, a experiencia también aporta aprendizaje.
- **Diseñar a prueba de errores:** no debemos asumir que las personas utilizarán un sistema de la manera esperada, hay que anticipar acciones inesperadas, errores y posibles problemas.
- **Parámetros:** permiten modificar el comportamiento de una función o un objeto según los valores que recibe, estos abren un universo de posibilidades al programar.

---

### Clases
Referencia: [W3Schools - C++ Classes](https://www.w3schools.com/cpp/cpp_classes.asp).

Así como existen tipos de datos como `char`, `int`, `bool` y `float`, en C++ también podemos crear nuestros propios tipos utilizando `class`.

Una clase es una plantilla que agrupa atributos y métodos relacionados con un objeto.

- **Atributos:** son las variables que representan las características o los datos de un objeto.
- **Métodos:** son las funciones que pertenecen a una clase y permiten realizar acciones.

También existen formas de proteger las variables y controlar quién puede acceder a ellas.

### Ejemplo de la clase `Termo`

```cpp
class Termo {
public:
    bool existencia;
    int posicion;
    int cantidadML;
    float temperature;

    void abrir();
    void cerrar();
};
```

En este ejemplo:
- `class Termo`: define una clase llamada `Termo`.
- `public:`: indica que los miembros declarados en esta sección son accesibles desde fuera de la clase.
- `bool existencia`: representa un valor verdadero o falso.
- `int posicion`: representa una posición mediante un número entero.
- `int cantidadML`: representa una cantidad en mililitros.
- `float temperature`: permite almacenar una temperatura con decimales.
- `void abrir();`: declara un método llamado `abrir()` que no devuelve un valor.
- `void cerrar();`: declara un método llamado `cerrar()` que tampoco devuelve un valor.

Los métodos están declarados, pero todavía es necesario definir qué acciones realizarán.

#### Modificadores de acceso
Permiten controlar quién puede utilizar los atributos y métodos de una clase.

| Modificador | Función                                                         |
| ----------- | --------------------------------------------------------------- |
| `public`    | Permite acceder a los miembros desde fuera de la clase.         |
| `private`   | Restringe el acceso directo desde fuera de la clase.            |
| `protected` | Permite el acceso desde la propia clase y sus clases derivadas. |

Por ejemplo, si declaramos un atributo como `private`, no podremos modificarlo directamente desde fuera de la clase. En su lugar, podemos crear métodos públicos para controlar cómo se utiliza.

### Constructores
Referencia: [W3Schools - C++ Constructors](https://www.w3schools.com/cpp/cpp_constructors.asp).

Un constructor es un método especial que se ejecuta automáticamente cuando creamos un objeto de una clase. Su función principal es inicializar los atributos del objeto.

**Características de los constructores:**
- Se llaman exactamente igual que la clase.
- No tienen tipo de retorno: no llevan `void`, `int` ni otro tipo.
- Pueden recibir parámetros.
- Puede haber más de un constructor en una misma clase, siempre que tengan listas de parámetros diferentes.

#### Ejemplo de constructor

```cpp
class Termo {
public:
    int cantidadML;

    Termo(int cantidad) {
        cantidadML = cantidad;
    }
};
```
En este caso, `Termo(int cantidad)` es el constructor.

Recibe un parámetro llamado `cantidad` y lo utiliza para asignar un valor al atributo `cantidadML`.

Podemos crear objetos utilizando ese constructor:
```cpp
Termo elDeCatalina(800);
Termo elDePedro(500);
```

- `elDeCatalina` comienza con `cantidadML = 800`.
- `elDePedro` comienza con `cantidadML = 500`

#### Parámetros del constructor
Los parámetros permiten entregar datos al objeto en el momento de su creación.

Esto hace posible crear varios objetos de una misma clase con diferentes valores, en lugar de que todos comiencen necesariamente con los mismos datos.

La clase funciona como una plantilla y cada objeto es una instancia creada a partir de ella.

#### Utilizar más de un constructor
Podemos definir diferentes constructores según nuestras necesidades. 

```cpp
class Termo {
public:
    int cantidadML;

    Termo() {
        cantidadML = 0;
    }

    Termo(int cantidad) {
        cantidadML = cantidad;
    }
};
```

En este ejemplo existen dos constructores:
- `Termo()`: no recibe parámetros e inicializa `cantidadML` en 0.
- `Termo(int cantidad)`: recibe un entero e inicializa `cantidadML` con ese valor.

Podemos utilizarlos de esta manera:

```cpp
Termo termoVacio;
Termo termoGrande(800);
```
El primero comienza con 0 y el segundo con 800.

La elección depende de cómo creamos el objeto y de los constructores disponibles en la clase.
