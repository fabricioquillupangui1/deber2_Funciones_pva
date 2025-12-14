 Funciones en Kotlin y Programación
La unidad básica de la modularidad y la reutilización del código.

1. ✨ ¿Qué son las Funciones (`fun`)?
Una función es un bloque de código reusable y con nombre que realiza una tarea específica. En Kotlin, se declaran con la palabra clave fun.

Son esenciales para la modularidad, la reutilización de código (Principio DRY) y para hacer el programa más legible.

Estructura Básica de una Función en Kotlin
Una función típicamente incluye Parámetros de Entrada, el Cuerpo de la Función (el proceso) y un Valor de Retorno (el resultado).

fun sumar(num1: Int, num2: Int): Int {
    // num1 y num2 son los parámetros
    val resultado = num1 + num2
    return resultado // Devuelve un valor de tipo Int
}

val total = sumar(10, 5) // Llamada con argumentos
2. 📝 Elementos Clave y Scope
A. Parámetros, Argumentos y Retorno
La diferencia entre Parámetro y Argumento es fundamental:

Concepto	Descripción	Ejemplo
Parámetro	Variable definida en la declaración de la función.	num1: Int en la definición.
Argumento	El valor real que se pasa al llamar la función.	10 al llamar sumar(10, 5).
Retorno	Tipo de valor que la función debe devolver. Si no devuelve nada, el tipo implícito es Unit.	: Int en la declaración.
Argumentos por Defecto: Permiten hacer los parámetros opcionales.

fun saludar(nombre: String = "Usuario", edad: Int) {
    println("Hola $nombre, tienes $edad años.")
}

saludar(edad = 30) // Usa el nombre por defecto: "Usuario"
B. Ámbito (Scope) de las Variables
El scope define la accesibilidad de las variables. Las variables declaradas dentro de una función son locales y no pueden ser vistas desde fuera.

// Variable Global (accesible por cualquier función)
val PI = 3.14159 

fun calcular(radio: Double) {
    // 'area' es una variable Local
    val area = PI * radio * radio 
    println("El área es $area")
}

// Error: 'area' no es accesible aquí. Su scope terminó con la función.
// val resultado = area 
3. 🧩 Tipos de Funciones en Kotlin
A. Funciones de Expresión Única
Ideales para funciones cortas donde solo hay una expresión de retorno. Ahorran código al omitir las llaves y la palabra return.

// Sintaxis simplificada, el tipo de retorno se infiere:
fun multiplicarCorta(a: Int, b: Int) = a * b 
B. Funciones de Extensión
Permiten añadir nuevas funcionalidades a clases existentes (como String, Int o tus propias clases) sin modificarlas. Esto hace que el código sea más legible y orientado a objetos.

// Agregamos la función 'esPar' a todos los objetos Int
fun Int.esPar(): Boolean { 
    return this % 2 == 0
}

// Uso:
val numero = 4
println(numero.esPar()) // Resultado: true
C. Funciones de Orden Superior y Lambdas
Son funciones que aceptan otras funciones como parámetro o que devuelven una función como resultado. Son la base de muchas operaciones con colecciones (map, filter) y en Jetpack Compose.

// La función 'forEach' toma una función Lambda como argumento
val lista = listOf(1, 2, 3)

lista.forEach { valor -> 
    println("Item: $valor") // La lambda se ejecuta por cada elemento
}
D. Funciones Infix (Notación Infija)
Permiten llamar a una función sin usar el punto ni los paréntesis, como si fueran operadores. Deben ser funciones de extensión o miembro y tomar exactamente **un solo parámetro**.

infix fun Int.multiplicadoPor(otro: Int): Int {
    return this * otro
}

// Uso normal (sintaxis de punto)
val r1 = 5.multiplicadoPor(3)

// Uso Infix (sintaxis sin punto ni paréntesis, más legible)
val r2 = 5 multiplicadoPor 3
// r2 es 15
E. Funciones Suspendidas (`suspend fun`)
Son fundamentales en el desarrollo de Android con Corrutinas. Una función `suspend` es una función que puede ser **pausada y reanudada** más tarde sin bloquear el hilo principal (UI). Se usan para tareas largas o asíncronas (redes, bases de datos).

// La función 'delay' solo puede ser llamada dentro de otra suspend fun o un CoroutineScope
suspend fun obtenerDatos(): String {
    delay(2000) // Pausa la ejecución por 2 segundos sin bloquear el hilo
    return "Datos cargados"
}

// Permite que el código asíncrono se vea y se escriba de forma secuencial.
F. Funciones Locales (Nested Functions)
Son funciones que se declaran dentro del cuerpo de otra función. Solo son visibles y accesibles desde la función contenedora, ayudando a encapsular la lógica compleja o repetitiva internamente.

fun validarYProcesar(input: String) {
    
    // Función anidada (Local)
    fun esValido(texto: String): Boolean {
        return texto.isNotEmpty()
    }

    if (esValido(input)) {
        println("Procesando input...")
    } else {
        println("Input inválido.")
    }
}
// Error: La función 'esValido' no es accesible fuera de 'validarYProcesar'
5. 📸 Galería Visual: Funciones en Acción
Esta sección complementa los ejemplos de código con diagramas y representaciones visuales que ayudan a comprender mejor los conceptos de las funciones en Kotlin y su aplicación en Android Compose.

Diagrama 1: Flujo Básico de una Función
Visualización del proceso de una función: entrada de parámetros, ejecución de lógica y retorno de un valor.



Diagrama 2: Función Nominal (Ej. Área del Círculo)
Representación visual de una función con parámetros y un retorno explícito, como el cálculo del área.



Diagrama 3: Funciones de Extensión en Kotlin
Cómo las funciones de extensión "añaden" comportamientos a clases existentes sin modificarlas directamente.



Diagrama 4: Argumentos por Defecto
Ilustración de cómo los argumentos por defecto hacen los parámetros opcionales en las funciones.



Diagrama 5: Funciones Locales y su Ámbito
Representación del concepto de "scope": funciones anidadas que solo son visibles dentro de su función contenedora.



Diagrama 6: 'when' como Expresión en Kotlin
Cómo la expresión `when` en Kotlin simplifica la lógica condicional compleja, actuando como un `switch` potente.



Diagrama 7: Función de Expresión Única (Concisión)
La forma más corta de escribir funciones en Kotlin para lógica simple, omitiendo `return` y corchetes.



4. 🎯 Ejercicios Prácticos en Android Compose
Estos ejercicios demuestran la aplicación de funciones en un contexto real de UI modular en Android, utilizando Kotlin y Jetpack Compose.

Ejercicio 1: Calculadora de Área del Círculo
Se puede trabajar en las unidades de centimetros y metros cuadrados depende de cada uno como se lo quiera usar

Conceptos Demostrados: Función Nominal (fun), Parámetros de Entrada, Retorno Explícito (return) y Constantes Globales (PI).

A. Función de Lógica (Cálculo Reutilizable)

// Importamos PI para usarlo como constante global
import kotlin.math.PI

/**
 * Función Nominal que calcula el área de un círculo.
 * @param radio: El valor del radio del círculo (parámetro).
 * @return El área calculada como un Double.
 */
fun calcularAreaCirculo(radio: Double): Double {
    // PI es una constante global accesible (Scope)
    val area = PI * radio * radio 
    return area // Retorno explícito del resultado
}
B. Implementación en la UI (Fragmento de la Composable)

/* La función principal para la pantalla */
@Composable
fun CalculadoraAreaCirculoScreen() {
    // Estado para guardar el texto introducido por el usuario
    var inputRadio by remember { mutableStateOf("") }
    var resultadoArea by remember { mutableStateOf("0.0") }

    // ... OutlinedTextField ...

    Button(
        onClick = {
            // Obtiene el valor, usando 0.0 como Argumento por defecto si es nulo
            val radio = inputRadio.toDoubleOrNull() ?: 0.0 
            
            // Llamada a la Función de Lógica Pura:
            val areaCalculada = calcularAreaCirculo(radio) 
            
            resultadoArea = String.format("%.2f", areaCalculada)
        }
    ) { Text("Calcular Área") }

    Text("Resultado (Área): $resultadoArea metros cuadrados")
}
Ejercicio 2: Verificador de Voto (Ecuador)
Conceptos Demostrados: Función Booleana (Retorna True/False), Expresión Única y Lógica Condicional Sencilla.

A. Función de Lógica (Verificación de Edad)

/**
 * Función de Expresión Única (la más sencilla).
 * Verifica si la edad cumple con el mínimo de 16 años de Ecuador.
 * El tipo de retorno (Boolean) se infiere.
 */
fun esElegible(edad: Int) = edad >= 16 
B. Implementación en la UI (Fragmento de la Composable)

@Composable
fun VerificadorVotoEcuadorScreen() {
    // ... Definición de Estados (edadInput, showDialog, resultadoTexto) ...

    Button(
        onClick = {
            val edad = edadInput.toIntOrNull() ?: 0 
            
            // Llamada a la Función Booleana:
            val esAceptado = esElegible(edad) 
            
            if (esAceptado) {
                resultadoTexto = "Puedes votar en las próximas elecciones, has sido aceptado."
            } else {
                resultadoTexto = "Lo sentimos, no cumples con la edad mínima (16 años) para votar."
            }
            showDialog = true 
        }
    ) { Text("Verificar") }

    // ... AlertDialog que usa resultadoTexto para mostrar el mensaje ...
}
Ejercicios prácticos y Readme (Dar click en los enlaces)
