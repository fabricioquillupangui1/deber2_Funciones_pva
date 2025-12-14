---

# 🚀 Funciones en Kotlin y Jetpack Compose

Este repositorio contiene una explicación clara, estructurada y práctica sobre las **funciones en Kotlin**, su importancia en la programación modular y su aplicación real en **Jetpack Compose** para Android.  
El objetivo es comprender cómo las **funciones** permiten organizar la lógica del programa, reutilizar código y controlar el comportamiento de la interfaz de usuario de forma eficiente.

---

## 🔹 1. ¿Qué son las Funciones (`fun`)?

Una función es un **bloque de código reutilizable** con un nombre definido que realiza una tarea específica.  
En Kotlin, las funciones se declaran utilizando la palabra clave `fun`.

### ¿Por qué son importantes?

* Permiten dividir programas grandes en partes pequeñas
* Evitan repetir código (Principio **DRY**)
* Mejoran la legibilidad y el mantenimiento del software
* Facilitan el trabajo en proyectos Android modernos

```kotlin
fun sumar(num1: Int, num2: Int): Int {
    val resultado = num1 + num2
    return resultado
}

val total = sumar(10, 5)
🔹 2. Elementos Clave de una Función
Parámetros, Argumentos y Retorno
Parámetro: Variable definida en la función

Argumento: Valor enviado al llamar la función

Retorno: Valor que devuelve la función (si no devuelve nada → Unit)

kotlin
Copiar código
fun saludar(nombre: String = "Usuario", edad: Int) {
    println("Hola $nombre, tienes $edad años.")
}

saludar(edad = 30)
🔹 3. Scope (Ámbito de las Variables)
El scope define dónde una variable puede ser utilizada.
Las variables declaradas dentro de una función son locales y solo existen dentro de ella.

kotlin
Copiar código
val PI = 3.14159

fun calcular(radio: Double) {
    val area = PI * radio * radio
    println("El área es $area")
}
🔹 4. Tipos de Funciones en Kotlin
🔸 Funciones de Expresión Única
Se usan cuando la función tiene una sola expresión de retorno.

kotlin
Copiar código
fun multiplicarCorta(a: Int, b: Int) = a * b
🔸 Funciones de Extensión
Permiten agregar funcionalidades a clases existentes sin modificarlas.

kotlin
Copiar código
fun Int.esPar(): Boolean {
    return this % 2 == 0
}

val numero = 4
println(numero.esPar())
🔸 Funciones de Orden Superior y Lambdas
Son funciones que reciben otras funciones como parámetro.

kotlin
Copiar código
val lista = listOf(1, 2, 3)

lista.forEach { valor ->
    println("Item: $valor")
}
🔸 Funciones Infix
Permiten una sintaxis más natural y legible.

kotlin
Copiar código
infix fun Int.multiplicadoPor(otro: Int): Int {
    return this * otro
}

val r1 = 5.multiplicadoPor(3)
val r2 = 5 multiplicadoPor 3
🔸 Funciones Suspendidas (suspend fun)
Se utilizan con corrutinas para ejecutar tareas largas sin bloquear el hilo principal.

kotlin
Copiar código
suspend fun obtenerDatos(): String {
    delay(2000)
    return "Datos cargados"
}
🔸 Funciones Locales (Nested Functions)
Son funciones declaradas dentro de otra función y solo accesibles desde ella.

kotlin
Copiar código
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
🔹 5. Ejercicios Prácticos en Jetpack Compose
🧮 Ejercicio 1: Calculadora de Área del Círculo
Conceptos demostrados:

Función nominal

Parámetros

Retorno explícito

Constantes globales

kotlin
Copiar código
import kotlin.math.PI

fun calcularAreaCirculo(radio: Double): Double {
    val area = PI * radio * radio
    return area
}
kotlin
Copiar código
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

Condicionales

kotlin
Copiar código
fun esElegible(edad: Int) = edad >= 16
kotlin
Copiar código
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
Las funciones en Kotlin son la base de la programación moderna.
Permiten crear aplicaciones modulares, reutilizables y mantenibles, y son esenciales para el desarrollo de interfaces reactivas con Jetpack Compose.
