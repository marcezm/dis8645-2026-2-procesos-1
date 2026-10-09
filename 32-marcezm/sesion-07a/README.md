# sesion-07a
Martes 29 de Septiembre

## apuntes sesión

```cpp
int main()
```
`main()` es la función principal del programa, indica el punto desde donde comienza la ejecución y contiene las instrucciones que se ejecutarán, directa o indirectamente, a través de otras funciones.

### Condicional `if` y `else`
Si `x` es mayor o igual a `y`, se retorna `x`.

```cpp
if (x >= y) {
    return x;
}
```
En caso contrario, se retorna `y`.

```cpp
else {
    return y;
}
```
Ambos bloques juntos permiten crear una función que determine cuál de los dos números es mayor:

```cpp
int cualEsMayor(int x, int y) {
    if (x >= y) {
        return x;
    } else {
        return y;
    }
}
```
- `if`: ejecuta instrucciones si se cumple una condición.
- `else`: ejecuta instrucciones cuando la condición del `if` no se cumple.
- `>=`: significa mayor o igual que.
- `return`: devuelve un valor desde la función.

En este caso, si ambos números son iguales, la función devuelve `x`.

### Botones y lectura de estados
Cuando el estado de un botón cambia de `0` a `1`, se produce un cambio importante: puede indicar que el botón pasó de estar suelto a estar presionado.

En una lectura digital habitual:
- `0`: nivel bajo (`LOW`).
- `1`: nivel alto (`HIGH`).

***Importante:** esto depende de cómo esté conectado el botón. En una conexión activa en bajo, los valores pueden interpretarse al revés.*

### Estructura general de una clase
La estructura macro que utilizaremos será la habitual de una clase en C++.

```cpp
class Nombre {
public:
    // Variables o atributos
    int numero;
    bool estado;
    char letra;

    // Constructor
    Nombre() {
        // Inicialización
    }

    // Métodos
    void abrir();
    void cerrar();
};
```

Una clase agrupa atributos y métodos relacionados con un objeto.
- **Atributos:** variables que almacenan información del objeto.
- **Constructor:** inicializa el objeto cuando se crea.
- **Métodos:** funciones que permiten realizar acciones.
- `public`: permite acceder a los miembros declarados en esa sección desde fuera de la clase.

En clases trabajaremos principalmente con `public`, aunque también existen `private` y `protected` para controlar el acceso.

### Constructores
Un constructor es un método especial que se ejecuta automáticamente al crear un objeto. Su función principal es inicializar los atributos.

#### Ejemplo general

```cpp
Nombre(int nombreCualquiera) {
    blabla = nombreCualquiera;
}
```

En este ejemplo:
- `Nombre`: tiene que coincidir con el nombre de la clase.
- `int nombreCualquiera`: recibe un parámetro entero.
- `blabla = nombreCualquiera;`: asigna el valor recibido al atributo `blabla`.

**El nombre `blabla` es solamente un ejemplo y tendría que corresponder a un atributo que exista en la clase**

#### Ejemplo con `Termo`

```cpp
Termo(int cuantosML) {
    cantidadML = cuantosML;
}
```
Este constructor recibe una cantidad en mililitros y la asigna al atributo `cantidadML`.

Por ejemplo:

```cpp
Termo elDeCatalina(800);
```
El objeto `elDeCatalina` se crea con el valor inicial `800` para `cantidadML`.

### Varios parámetros en un constructor
Puede haber más de un parámetro en el mismo constructor.

```cpp
Termo(int cuantosML, float temperaturaInicial) {
    cantidadML = cuantosML;
    temperatura = temperaturaInicial;
}
```
En este caso, el constructor recibe dos valores: la cantidad de mililitros y la temperatura inicial.

También puede haber varios constructores dentro de una misma clase, siempre que sus listas de parámetros sean diferentes.

### Métodos
Los métodos son funciones asociadas a una clase, permiten definir las acciones que puede realizar un objeto.

#### Métodos para abrir y cerrar

```cpp
// Métodos para abrir y cerrar

void abrir() {
    abierto = true;
}

void cerrar() {
    abierto = false;
}
```

- `void`: indica que el método no devuelve un valor.
- `abrir()`: cambia el atributo `abierto` a `true`.
- `cerrar()`: cambia el atributo `abierto` a `false`.

Para que estos métodos funcionen, la clase debe tener un atributo llamado `abierto`, por ejemplo, `bool abierto = false;`

#### Método para enfriar

```cpp
// Método para enfriar

void enfriar() {
    temperatura = temperatura - 0.7;
}
```
Este método disminuye el valor del atributo `temperatura` en `0.7` cada vez que se ejecuta.

Para que funcione, debe existir un atributo llamado `temperatura`, por ejemplo, de tipo `float`.

---

> `%.1f` es un especificador de formato que se utiliza con `printf()` para mostrar un número decimal con un solo dígito después del punto.

```cpp
float temperatura = 18.75;

printf("Temperatura: %.1f\n", temperatura);
```

Resultado:
```text
Temperatura: 18.8
```

- `%`: comienza el especificador de formato.
- `.1`: indica que se mostrará un decimal.
- `f`: indica un número de punto flotante.

El valor se redondea para mostrar la cantidad de decimales solicitada.

---

### Diferencias entre `float` y `double`
- `float`: permite almacenar números de punto flotante con una precisión limitada.
- `double`: permite almacenar números de punto flotante con mayor precisión.

Los números de punto flotante pueden tener pequeñas diferencias de representación porque muchos valores decimales no pueden almacenarse de forma exacta en formato binario.

Por eso a veces aparecen aproximaciones inesperadas al realizar operaciones con ellos.

### Clase `Boton`
En clases comenzamos a construir una clase que representa un botón y sus características.

```cpp
class Boton {
public:
    // Atributos
    bool presionado = 0;
    uint duracionPresionado = 0;
    int patita;
    int vecesPresionado = 0;
    char[] nombre;

    // Constructor
    Boton(int nuevaPatita) {
        patita = nuevaPatita;
    }

    // Métodos
    void
};
```

### Explicación de los atributos

- `bool presionado = 0;`: indica si el botón está presionado. `0` representa `false`.
- `uint duracionPresionado = 0;`: almacena la duración de la pulsación como un entero sin signo, en los entornos donde `uint` está definido.
- `int patita;`: almacena el número del pin al que está conectado el botón.
- `int vecesPresionado = 0;`: cuenta cuántas veces se ha presionado.
- `nombre`: busca representar el nombre del botón, pero la declaración `char[] nombre;` no es válida en este contexto de C++. Hay otras formas de almacenar un nombre, como `const char* nombre;` o `std::string nombre;`.

#### ¿Qué significa la `u` en `uint`?
La `u` hace referencia a unsigned es decir un número entero sin signo.

Un entero sin signo no puede representar valores negativos. Se utiliza cuando los valores que necesitamos almacenar son cero o positivos, como un contador o una duración.

Hay que tener presente que `uint` no es un tipo estándar universal de C++; su disponibilidad depende del entorno o de las bibliotecas utilizadas.

### Constructor de `Boton`

```cpp
Boton(int nuevaPatita) {
    patita = nuevaPatita;
}
```
El constructor recibe el número del pin y lo guarda en el atributo `patita`.

De esta manera, podemos crear distintos botones con diferentes pines:

```cpp
Boton pausa(GP1);
Boton reproducir(GP3);
Boton apagar(GP30);
```
Cada objeto tiene un nombre diferente y recibe un pin distinto.

Los identificadores `GP1`, `GP3` y `GP30` deben estar definidos y corresponder a pines válidos en la placa que estamos utilizando.

### Métodos de la clase

Los métodos permiten indicar qué acciones puede realizar un botón. Por ejemplo, detectar si está presionado, registrar cuánto tiempo se mantiene presionado o contar sus pulsaciones.

La declaración incompleta `void` del código original indica que todavía faltaba definir el nombre y el contenido del método.

---

### Diferencia entre los archivos `.h` y `.cpp`
Para organizar el código, podemos separar la declaración de una clase de la implementación de sus métodos.

#### Archivo `.h`
El archivo de cabecera indica qué atributos, constructores y métodos forman parte de la clase.

Por ejemplo:
```cpp
// Boton.h

class Boton {
public:
    bool presionado = false;
    int patita;

    Boton(int nuevaPatita);

    void abrir();
    void cerrar();
};
```

#### Archivo `.cpp`
El archivo de implementación contiene las instrucciones que explican cómo funcionan los métodos.

```cpp
// Boton.cpp

#include "Boton.h"

Boton::Boton(int nuevaPatita) {
    patita = nuevaPatita;
}

void Boton::abrir() {
    presionado = true;
}

void Boton::cerrar() {
    presionado = false;
}
```

En este ejemplo:
- `Boton.h` declara los miembros de la clase.
- `Boton.cpp` implementa el constructor y los métodos.
- `Boton::abrir()` indica que el método `abrir()` pertenece a la clase `Boton`.
- `Boton::cerrar()` indica que el método `cerrar()` pertenece a la clase `Boton`.

**Importante:** las funciones que aparecen en `Boton.cpp` deben estar declaradas de forma compatible con la clase definida en `Boton.h`.

La ventaja de esta organización es que el archivo `.h` queda más corto y permite consultar rápidamente qué puede hacer la clase, mientras que el `.cpp` contiene los detalles de cómo se realizan esas acciones.

### Referencias de la clase
* [Grupo.h — GitHub](https://github.com/disenoUDP/dis8645-2025-2-procesos/blob/main/00-metaclases/Grupo.h)
* [Grupo.cpp — GitHub](https://github.com/disenoUDP/dis8645-2025-2-procesos/blob/main/00-metaclases/Grupo.cpp)

---

### Código en crudo de Wokwi
Este es el código del ejercicio que utilizamos para probar la lectura de un botón conectado a la Raspberry Pi Pico.

```cpp
// Esto venía en Wokwi

#include <stdio.h>
#include "pico/stdlib.h"

// Esto lo agregamos para GPIO
// General Purpose Input/Output
#include "hardware/gpio.h"

// Incluir mis archivos
#include "Boton.h"

int main() {

    stdio_init_all();

    // Inicializar patita 7
    gpio_init(7);

    // La patita 7 es entrada
    gpio_set_dir(7, GPIO_IN);

    // Crear Boton
    // Que se llama miPrimerBoton
    // Con el constructor

    // Había hecho un error:
    // usar paréntesis sin nada,
    // que no son necesarios cuando
    // el constructor no tiene parámetros

    // Boton miPrimerBoton();
    Boton miPrimerBoton;

    while (true) {

        // Leer botón
        bool lectura = gpio_get(7);

        if (lectura) {
            printf("caramba estoy presionado\n");
        } else {
            printf("pucha no hay nadie\n");
        }

        // digitalRead();

        // if (miPrimerBoton.presionado) {
        //     printf("bacán estoy presionado, pero igual me presiona\n");
        //     printf("o como dice Matías, estoy impresionado jaja\n");
        //     miPrimerBoton.soltar();
        // }
        // else {
        //     // Cuando no esté presionado
        //     printf("no hay nadie presionándome\n");
        //     miPrimerBoton.presionar();
        // }

        // printf("Hello, Wokwi!\n");
        sleep_ms(1000);
    }
}
```
#### Inicialización del pin
```cpp
gpio_init(7);
gpio_set_dir(7, GPIO_IN);
```

- `gpio_init(7);`: inicializa el GPIO número 7.
- `gpio_set_dir(7, GPIO_IN);`: configura ese pin como entrada para leer una señal externa.

GPIO significa *General Purpose Input/Output*, es decir, entrada/salida de propósito general.

#### Leer el botón
```cpp
bool lectura = gpio_get(7);
```
Esta instrucción lee el estado digital del pin 7 y guarda el resultado en la variable `lectura`.

Como se utiliza `bool`, el estado se interpreta como verdadero o falso.

#### Condicional para mostrar el estado
```cpp
if (lectura) {
    printf("caramba estoy presionado\n");
} else {
    printf("pucha no hay nadie\n");
}
```
Si `lectura` es verdadera, muestra el primer mensaje. Si es falsa, muestra el segundo.

La interpretación depende de la conexión eléctrica del botón. Si el circuito utiliza una resistencia *pull-up*, por ejemplo, el nivel bajo puede corresponder a la pulsación.

#### Pausa del programa
```cpp
sleep_ms(1000);
```
Hace una pausa de 1000 milisegundos, equivalente a un segundo, antes de volver a leer el botón.

#### Error al crear un objeto
En el código original aparece esta línea comentada:

```cpp
// Boton miPrimerBoton();
```

En C++, esa sintaxis puede interpretarse como una declaración de función en lugar de crear un objeto. Por eso, cuando queremos crear un objeto con un constructor sin parámetros, escribimos:

```cpp
Boton miPrimerBoton;
```

Sin embargo, en la clase `Boton` que anotamos anteriormente solo aparece un constructor que recibe un parámetro (`Boton(int nuevaPatita)`). Para que `Boton miPrimerBoton;` funcione, la clase debe tener también un constructor sin parámetros o debe crearse el objeto entregando el pin correspondiente.

Además, el código de Wokwi todavía lee directamente el GPIO con `gpio_get(7)`. Aunque crea un objeto `miPrimerBoton`, todavía no utiliza sus atributos ni sus métodos para gestionar la pulsación.

## encargos

1. usar el ejemplo base visto en clases <https://wokwi.com/projects/476507507193136129>, agregar un segundo botón en la simulación de hardware, agregar una segunda instancia de la clase Boton, agregarle un atributo y un método a la clase Boton, y hacer que el segundo botón haga algo diferente al primero.
2. descargar todos los archivos de wokwi, descomprimir el archivo.zip y subir esa carpeta a tu repositorio en esta sesión.

## lectura
