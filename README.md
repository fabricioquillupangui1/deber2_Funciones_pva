📘 Funciones en Kotlin y Programación

La unidad básica de la modularidad y la reutilización del código en Kotlin son las funciones.
Este documento explica qué son, cómo se usan y cómo se aplican en Android con Jetpack Compose, combinando teoría clara y ejercicios prácticos.

✨ 1. ¿Qué son las Funciones (fun)?

Una función es un bloque de código reutilizable y con nombre que realiza una tarea específica.
En Kotlin, las funciones se declaran usando la palabra clave fun.

Las funciones son esenciales porque permiten:

Modularizar el código

Reutilizar lógica (Principio DRY: Don't Repeat Yourself)

Mejorar la legibilidad y el mantenimiento del programa

📌 Estructura básica de una función en Kotlin

Una función normalmente contiene:

Parámetros de entrada

Cuerpo de la función (la lógica)

Valor de retorno

fun sumar(num1: Int, num2: Int): Int {
    // num1 y num2 son los parámetros
    val resultado = num1 + num2
    return resultado // Devuelve un valor de tipo Int
}

val total = sumar(10, 5) // Llamada con argumentos

📝 2. Elementos Clave y Scope
A. Parámetros, Argumentos y Retorno

Es importante diferenciar estos conceptos:

Concepto	Descripción	Ejemplo
Parámetro	Variable definida en la función	num1: Int
Argumento	Valor real enviado a la función	10 en sumar(10, 5)
Retorno	Valor que la función devuelve	: Int
🔹 Argumentos por defecto

Permiten hacer parámetros opcionales:

fun saludar(nombre: String = "Usuario", edad: Int) {
    println("Hola $nombre, tienes $edad años.")
}

saludar(edad = 30)

B. Ámbito (Scope) de las Variables

El scope define dónde una variable es accesible.

Variables globales: accesibles desde cualquier función

Variables locales: solo existen dentro de la función donde se declaran

val PI = 3.14159 // Variable global

fun calcular(radio: Double) {
    val area = PI * radio * radio // Variable local
    println("El área es $area")
}

// Error: 'area' no es accesible fuera de la función

🧩 3. Tipos de Funciones en Kotlin
A. Funciones de Expresión Única

Son funciones cortas que retornan una sola expresión.

fun multiplicarCorta(a: Int, b: Int) = a * b

B. Funciones de Extensión

Permiten agregar funciones a clases existentes sin modificarlas.

fun Int.esPar(): Boolean {
    return this % 2 == 0
}

val numero = 4
println(numero.esPar()) // true

C. Funciones de Orden Superior y Lambdas

Son funciones que reciben otras funciones como parámetro o las devuelven.

val lista = listOf(1, 2, 3)

lista.forEach { valor ->
    println("Item: $valor")
}

D. Funciones Infix (Notación Infija)

Permiten llamar funciones sin usar punto ni paréntesis.
Requisitos:

Ser función de extensión o miembro

Tener un solo parámetro

infix fun Int.multiplicadoPor(otro: Int): Int {
    return this * otro
}

val r1 = 5.multiplicadoPor(3)
val r2 = 5 multiplicadoPor 3

E. Funciones Suspendidas (suspend fun)

Se usan con corrutinas en Android para tareas largas o asíncronas sin bloquear la interfaz.

suspend fun obtenerDatos(): String {
    delay(2000)
    return "Datos cargados"
}

F. Funciones Locales (Nested Functions)

Son funciones declaradas dentro de otra función.
Solo existen dentro de su función contenedora.

fun validarYProcesar(input: String) {

    fun esValido(texto: String): Boolean {
        return texto.isNotEmpty()
    }

    if (esValido(input)) {
        println("Procesando input...")
    } else {
        println("Input inválido.")
    }
}

📸 4. Galería Visual: Funciones en Acción (Descripción)

Esta sección complementa los ejemplos de código con representaciones conceptuales como:

Flujo básico de una función

Funciones con retorno explícito

Funciones de extensión

Argumentos por defecto

Funciones locales y su ámbito

Expresiones when

Funciones de expresión única

(Las imágenes no se incluyen en este README)

🎯 5. Ejercicios Prácticos en Android Compose
🧮 Ejercicio 1: Calculadora de Área del Círculo

Conceptos demostrados:

Función nominal

Parámetros

Retorno explícito

Uso de constantes globales

A. Función de lógica
import kotlin.math.PI

fun calcularAreaCirculo(radio: Double): Double {
    val area = PI * radio * radio
    return area
}

B. Implementación en la UI (Composable)
@Composable
fun CalculadoraAreaCirculoScreen() {
    var inputRadio by remember { mutableStateOf("") }
    var resultadoArea by remember { mutableStateOf("0.0") }

    Button(
        onClick = {
            val radio = inputRadio.toDoubleOrNull() ?: 0.0
            val areaCalculada = calcularAreaCirculo(radio)
            resultadoArea = String.format("%.2f", areaCalculada)
        }
    ) {
        Text("Calcular Área")
    }

    Text("Resultado (Área): $resultadoArea metros cuadrados")
}

🗳️ Ejercicio 2: Verificador de Voto (Ecuador)

Conceptos demostrados:

Función booleana

Expresión única

Lógica condicional

A. Función de lógica
fun esElegible(edad: Int) = edad >= 16

B. Implementación en la UI (Composable)
@Composable
fun VerificadorVotoEcuadorScreen() {

    Button(
        onClick = {
            val edad = edadInput.toIntOrNull() ?: 0
            val esAceptado = esElegible(edad)

            if (esAceptado) {
                resultadoTexto = "Puedes votar en las próximas elecciones, has sido aceptado."
            } else {
                resultadoTexto = "Lo sentimos, no cumples con la edad mínima (16 años) para votar."
            }

            showDialog = true
        }
    ) {
        Text("Verificar")
    }
}

✅ Conclusión

Las funciones en Kotlin permiten escribir código:

Más limpio

Más reutilizable

Más fácil de mantener

Su uso es fundamental tanto en programación general como en el desarrollo de Android con Jetpack Compose, donde la modularidad y la claridad son claves.
