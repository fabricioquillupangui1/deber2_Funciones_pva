🚀 FUNCIONES EN KOTLIN Y PROGRAMACIÓN  
📱 Aplicación práctica en Android con Jetpack Compose

Este repositorio está enfocado en el **tema principal: FUNCIONES EN KOTLIN**, explicadas de forma clara, progresiva y aplicada al desarrollo de interfaces modernas con **Jetpack Compose**.  
El objetivo es comprender cómo las funciones permiten construir código **modular**, **reutilizable**, **legible** y **mantenible**, tanto en la lógica como en la interfaz de usuario.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 OBJETIVO DEL REPOSITORIO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
- Comprender qué son las funciones en Kotlin
- Diferenciar parámetros, argumentos y retorno
- Conocer el scope (ámbito) de las variables
- Identificar los distintos tipos de funciones
- Aplicar funciones en ejercicios reales con Android Compose

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✨ 1. ¿QUÉ SON LAS FUNCIONES (fun)?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Una función es un **bloque de código reutilizable** con un nombre específico que realiza una tarea concreta.  
En Kotlin, se declaran usando la palabra clave `fun`.

📌 Importancia de las funciones:
- Dividen el programa en partes pequeñas
- Evitan la repetición de código (Principio DRY)
- Mejoran la organización y la lectura del código
- Facilitan el mantenimiento del software

📌 Estructura básica de una función:

fun sumar(num1: Int, num2: Int): Int {
    val resultado = num1 + num2
    return resultado
}

val total = sumar(10, 5)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧱 2. ELEMENTOS CLAVE Y SCOPE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔹 Parámetro: variable definida en la función  
🔹 Argumento: valor enviado al llamar la función  
🔹 Retorno: valor que devuelve la función (si no devuelve nada → Unit)

Ejemplo con argumentos por defecto:

fun saludar(nombre: String = "Usuario", edad: Int) {
    println("Hola $nombre, tienes $edad años.")
}

saludar(edad = 30)

🔐 Scope (Ámbito de las variables):
Las variables declaradas dentro de una función solo existen allí.

val PI = 3.14159

fun calcular(radio: Double) {
    val area = PI * radio * radio
    println("El área es $area")
}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 3. TIPOS DE FUNCIONES EN KOTLIN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔹 A. Funciones de Expresión Única  
Usadas cuando solo existe una expresión de retorno.

fun multiplicarCorta(a: Int, b: Int) = a * b

🔹 B. Funciones de Extensión  
Agregan comportamiento a clases existentes.

fun Int.esPar(): Boolean {
    return this % 2 == 0
}

val numero = 4
println(numero.esPar())

🔹 C. Funciones de Orden Superior y Lambdas  
Funciones que reciben otras funciones como parámetro.

val lista = listOf(1, 2, 3)

lista.forEach { valor ->
    println("Item: $valor")
}

🔹 D. Funciones Infix  
Permiten una sintaxis más natural y legible.

infix fun Int.multiplicadoPor(otro: Int): Int {
    return this * otro
}

val r1 = 5.multiplicadoPor(3)
val r2 = 5 multiplicadoPor 3

🔹 E. Funciones Suspendidas (suspend fun)  
Usadas con corrutinas para tareas asíncronas sin bloquear la UI.

suspend fun obtenerDatos(): String {
    delay(2000)
    return "Datos cargados"
}

🔹 F. Funciones Locales (Nested Functions)  
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

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 4. EJERCICIOS PRÁCTICOS EN JETPACK COMPOSE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🧮 EJERCICIO 1: CALCULADORA DE ÁREA DEL CÍRCULO  
Conceptos aplicados:
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

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🗳️ EJERCICIO 2: VERIFICADOR DE VOTO (ECUADOR)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Conceptos aplicados:
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

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ CONCLUSIÓN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Las **funciones en Kotlin** son el pilar de la programación moderna.  
Permiten crear aplicaciones **modulares**, **reutilizables** y **claras**, siendo esenciales para el desarrollo profesional de aplicaciones Android con **Jetpack Compose**.

📌 Dominar las funciones es el primer paso hacia arquitecturas limpias y aplicaciones escalables.
