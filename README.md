Este repositorio contiene una explicación clara, estructurada y práctica sobre las funciones en Kotlin, su importancia en la programación modular y su aplicación real en Jetpack Compose para Android. El objetivo es comprender cómo las funciones permiten organizar el código, reutilizar lógica y construir interfaces limpias y mantenibles.

✨ 1. ¿Qué son las Funciones (fun)?
Una función es un bloque de código reutilizable y con nombre que realiza una tarea específica. En Kotlin se declaran utilizando la palabra clave fun.

Las funciones son fundamentales porque:
- Permiten dividir un programa grande en partes pequeñas
- Evitan repetir código (Principio DRY)
- Mejoran la legibilidad y el mantenimiento del software

Estructura básica de una función en Kotlin:
Una función normalmente incluye parámetros de entrada, un cuerpo donde se procesa la lógica y un valor de retorno.

fun sumar(num1: Int, num2: Int): Int {
    val resultado = num1 + num2
    return resultado
}

val total = sumar(10, 5)

📝 2. Elementos Clave y Scope

A. Parámetros, Argumentos y Retorno
Parámetro: Variable definida en la función (num1: Int).
Argumento: Valor enviado al llamar la función (10 en sumar(10, 5)).
Retorno: Tipo de dato que devuelve la función. Si no devuelve nada, el tipo es Unit.

Argumentos por defecto:
Permiten que un parámetro tenga un valor inicial y sea opcional.

fun saludar(nombre: String = "Usuario", edad: Int) {
    println("Hola $nombre, tienes $edad años.")
}

saludar(edad = 30)

B. Ámbito (Scope) de las Variables
El scope define dónde una variable es accesible. Las variables declaradas dentro de una función son locales.

val PI = 3.14159

fun calcular(radio: Double) {
    val area = PI * radio * radio
    println("El área es $area")
}

🧩 3. Tipos de Funciones en Kotlin

A. Funciones de Expresión Única
Se usan cuando la función tiene una sola expresión de retorno.

fun multiplicarCorta(a: Int, b: Int) = a * b

B. Funciones de Extensión
Permiten añadir funciones a clases existentes sin modificarlas.

fun Int.esPar(): Boolean {
    return this % 2 == 0
}

val numero = 4
println(numero.esPar())

C. Funciones de Orden Superior y Lambdas
Son funciones que reciben otras funciones como parámetro.

val lista = listOf(1, 2, 3)

lista.forEach { valor ->
    println("Item: $valor")
}

D. Funciones Infix
Permiten llamar funciones sin punto ni paréntesis, haciendo el código más legible.

infix fun Int.multiplicadoPor(otro: Int): Int {
    return this * otro
}

val r1 = 5.multiplicadoPor(3)
val r2 = 5 multiplicadoPor 3

E. Funciones Suspendidas (suspend fun)
Se utilizan con corrutinas para ejecutar tareas largas sin bloquear el hilo principal.

suspend fun obtenerDatos(): String {
    delay(2000)
    return "Datos cargados"
}

F. Funciones Locales (Nested Functions)
Son funciones declaradas dentro de otra función y solo accesibles desde ella.

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

🎯 4. Ejercicios Prácticos en Jetpack Compose

🧮 Ejercicio 1: Calculadora de Área del Círculo
Conceptos utilizados:
- Función nominal
- Parámetros
- Retorno explícito
- Constantes globales

Función de lógica:

import kotlin.math.PI

fun calcularAreaCirculo(radio: Double): Double {
    val area = PI * radio * radio
    return area
}

Implementación en la UI:

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
Conceptos utilizados:
- Función booleana
- Expresión única
- Condicionales

Función de lógica:

fun esElegible(edad: Int) = edad >= 16

Implementación en la UI:

@Composable
fun VerificadorVotoEcuadorScreen() {

    Button(
        onClick = {
            val edad = edadInput.toIntOrNull() ?: 0
            val esAceptado = esElegible(edad)

            resultadoTexto = if (esAceptado) {
                "Puedes votar en las próximas elecciones, has sido aceptado."
            } else {
                "Lo sentimos, no cumples con la edad mínima (16 años) para votar."
            }

            showDialog = true
        }
    ) {
        Text("Verificar")
    }
}

✅ Conclusión
Las funciones en Kotlin son la base de la programación moderna. Permiten crear código modular, reutilizable y fácil de mantener, y son esenciales para el desarrollo de aplicaciones Android con Jetpack Compose.
