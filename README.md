🚀🚀🚀  FUNCIONES EN KOTLIN Y PROGRAMACIÓN  🚀🚀🚀
════════════════════════════════════════════════════
📱 Desarrollo modular y reutilizable con Jetpack Compose

Este repositorio está centrado en el **tema principal: FUNCIONES EN KOTLIN**, explicadas de forma clara, visual y aplicada al desarrollo de aplicaciones Android modernas con **Jetpack Compose**.  
El objetivo es entender cómo las funciones organizan la lógica del programa y controlan el comportamiento de la interfaz de usuario.

---

🎯 OBJETIVO DEL REPOSITORIO
• Comprender qué son las funciones en Kotlin  
• Identificar parámetros, argumentos y valores de retorno  
• Entender el scope (ámbito) de las variables  
• Conocer los distintos tipos de funciones  
• Aplicar funciones en ejercicios reales con Android Compose  

---

✨ ¿QUÉ SON LAS FUNCIONES (fun)?
Una función es un **bloque de código reutilizable** que realiza una tarea específica.  
En Kotlin se declaran con la palabra clave `fun`.

📌 ¿Por qué son importantes?
• Permiten dividir programas grandes en partes pequeñas  
• Evitan repetir código (Principio DRY)  
• Mejoran la lectura y mantenimiento del código  

Ejemplo básico de una función:

fun sumar(num1: Int, num2: Int): Int {
    val resultado = num1 + num2
    return resultado
}

val total = sumar(10, 5)

---

🧱 ELEMENTOS CLAVE Y SCOPE

🔹 Parámetro: variable definida en la función  
🔹 Argumento: valor enviado al llamar la función  
🔹 Retorno: valor que devuelve la función (si no hay retorno → Unit)

Ejemplo con argumentos por defecto:

fun saludar(nombre: String = "Usuario", edad: Int) {
    println("Hola $nombre, tienes $edad años.")
}

saludar(edad = 30)

🔐 Scope (Ámbito de variables):
Las variables locales solo existen dentro de la función donde se declaran.

val PI = 3.14159

fun calcular(radio: Double) {
    val area = PI * radio * radio
    println("El área es $area")
}

---

🧩 TIPOS DE FUNCIONES EN KOTLIN

🔸 Funciones de expresión única  
Se usan cuando la función tiene una sola expresión.

fun multiplicarCorta(a: Int, b: Int) = a * b

🔸 Funciones de extensión  
Permiten agregar funcionalidades a clases existentes.

fun Int.esPar(): Boolean {
    return this % 2 == 0
}

val numero = 4
println(numero.esPar())

🔸 Funciones de orden superior y lambdas  
Reciben funciones como parámetros.

val lista = listOf(1, 2, 3)

lista.forEach { valor ->
    println("Item: $valor")
}

🔸 Funciones infix  
Hacen el código más natural y legible.

infix fun Int.multiplicadoPor(otro: Int): Int {
    return this * otro
}

val r1 = 5.multiplicadoPor(3)
val r2 = 5 multiplicadoPor 3

🔸 Funciones suspendidas (suspend fun)  
Permiten ejecutar tareas asíncronas sin bloquear la UI.

suspend fun obtenerDatos(): String {
    delay(2000)
    return "Datos cargados"
}

🔸 Funciones locales (Nested Functions)  
Funciones definidas dentro de otra función.

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

---

🎯 EJERCICIOS PRÁCTICOS EN JETPACK COMPOSE

🧮 Ejercicio 1: Calculadora de Área del Círculo  
Conceptos aplicados:
• Función nominal  
• Parámetros  
• Retorno explícito  
• Constantes globales  

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

---

🗳️ Ejercicio 2: Verificador de Voto (Ecuador)  
Conceptos aplicados:
• Función booleana  
• Expresión única  
• Condicionales  

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

---

✅ CONCLUSIÓN
Las **funciones en Kotlin** son la base de la programación moderna.  
Permiten crear código **ordenado**, **reutilizable** y **escalable**, siendo esenciales para el desarrollo de aplicaciones Android con **Jetpack Compose**.

📌 Dominar las funciones es un paso clave para construir aplicaciones profesionales.
