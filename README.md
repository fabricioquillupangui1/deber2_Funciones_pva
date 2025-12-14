████████████████████████████████████████████████████████
🚀🚀🚀  FUNCIONES EN KOTLIN Y PROGRAMACIÓN  🚀🚀🚀
████████████████████████████████████████████████████████
✨ Modularidad • Reutilización • Android • Jetpack Compose ✨

Bienvenido a este repositorio dedicado al **tema central: FUNCIONES EN KOTLIN**.  
Aquí encontrarás una explicación **visual, moderna y práctica** sobre cómo las funciones permiten construir aplicaciones Android **claras, ordenadas y profesionales**, integrando lógica y UI con **Jetpack Compose**.

────────────────────────────────────────────────────────
🎯 PROPÓSITO DEL REPOSITORIO
────────────────────────────────────────────────────────
✔ Entender qué son las funciones en Kotlin  
✔ Aprender a usar parámetros, argumentos y retornos  
✔ Comprender el scope de las variables  
✔ Identificar los principales tipos de funciones  
✔ Aplicar funciones en escenarios reales de Android  

────────────────────────────────────────────────────────
✨ ¿QUÉ ES UNA FUNCIÓN EN KOTLIN?
────────────────────────────────────────────────────────
Una función es un **bloque de código reutilizable** que ejecuta una tarea específica.  
En Kotlin, se declara usando la palabra clave `fun`.

💡 ¿Por qué son tan importantes?
• Organizan el código  
• Evitan duplicaciones (DRY)  
• Facilitan el mantenimiento  
• Mejoran la lectura del programa  

📌 Ejemplo básico:

fun sumar(num1: Int, num2: Int): Int {
    val resultado = num1 + num2
    return resultado
}

val total = sumar(10, 5)

────────────────────────────────────────────────────────
🧱 ELEMENTOS FUNDAMENTALES Y SCOPE
────────────────────────────────────────────────────────
🔹 Parámetro → Variable definida en la función  
🔹 Argumento → Valor real enviado a la función  
🔹 Retorno → Valor que devuelve la función  

📎 Argumentos por defecto:

fun saludar(nombre: String = "Usuario", edad: Int) {
    println("Hola $nombre, tienes $edad años.")
}

saludar(edad = 30)

🔐 Scope (Ámbito de las variables):
Las variables locales solo existen dentro de la función.

val PI = 3.14159

fun calcular(radio: Double) {
    val area = PI * radio * radio
    println("El área es $area")
}

────────────────────────────────────────────────────────
🧩 TIPOS DE FUNCIONES EN KOTLIN
────────────────────────────────────────────────────────

🔸 Funciones de expresión única  
Código corto, limpio y legible.

fun multiplicarCorta(a: Int, b: Int) = a * b

🔸 Funciones de extensión  
Agregan comportamiento a clases existentes.

fun Int.esPar(): Boolean {
    return this % 2 == 0
}

val numero = 4
println(numero.esPar())

🔸 Funciones de orden superior y lambdas  
Funciones que reciben funciones.

val lista = listOf(1, 2, 3)

lista.forEach { valor ->
    println("Item: $valor")
}

🔸 Funciones infix  
Lectura natural y elegante.

infix fun Int.multiplicadoPor(otro: Int): Int {
    return this * otro
}

val r1 = 5.multiplicadoPor(3)
val r2 = 5 multiplicadoPor 3

🔸 Funciones suspendidas (suspend fun)  
Ejecución asíncrona sin bloquear la UI.

suspend fun obtenerDatos(): String {
    delay(2000)
    return "Datos cargados"
}

🔸 Funciones locales (Nested Functions)  
Encapsulan lógica dentro de otra función.

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

────────────────────────────────────────────────────────
🎯 EJERCICIOS PRÁCTICOS CON JETPACK COMPOSE
────────────────────────────────────────────────────────

🧮 EJERCICIO 1: CALCULADORA DE ÁREA DEL CÍRCULO  
📚 Conceptos:
• Funciones  
• Parámetros  
• Retorno explícito  
• Constantes globales  

🔹 Función de lógica:

import kotlin.math.PI

fun calcularAreaCirculo(radio: Double): Double {
    val area = PI * radio * radio
    return area
}

🔹 Implementación UI:

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

────────────────────────────────────────────────────────
🗳️ EJERCICIO 2: VERIFICADOR DE VOTO (ECUADOR)
────────────────────────────────────────────────────────
📚 Conceptos:
• Función booleana  
• Expresión única  
• Condicionales  

🔹 Función de lógica:

fun esElegible(edad: Int) = edad >= 16

🔹 Implementación UI:

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

────────────────────────────────────────────────────────
🌟 CONCLUSIÓN
────────────────────────────────────────────────────────
Las **funciones en Kotlin** son el corazón de la programación moderna.  
Permiten crear aplicaciones **modulares**, **limpias** y **escalables**, fundamentales en Android con **Jetpack Compose**.

🔥 Dominar las funciones es dar el primer paso hacia aplicaciones profesionales y bien estructuradas.
