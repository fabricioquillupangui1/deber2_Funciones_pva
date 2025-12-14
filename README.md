Funciones en Kotlin y Programación Modular

Este documento abarca la teoría fundamental de las funciones en Kotlin, su estructura básica, los tipos de funciones avanzadas y la aplicación práctica de estos conceptos en ejercicios de Jetpack Compose.

---

## 1. ✨ Fundamentos: ¿Qué son las Funciones (`fun`)?

Una función es un bloque de código reusable y con nombre que realiza una tarea específica. En Kotlin, se declaran con la palabra clave `fun`. Son la unidad básica de la modularidad y la reutilización del código (Principio DRY).

### Estructura Básica de una Función en Kotlin

Una función incluye **Parámetros de Entrada**, el **Cuerpo de la Función** (la lógica) y un **Valor de Retorno** (el resultado).


```kotlin
fun sumar(num1: Int, num2: Int): Int {
    // num1 y num2 son los parámetros
    val resultado = num1 + num2
    return resultado // Devuelve un valor de tipo Int
}
val total = sumar(10, 5) // Llamada con argumentos
2. 📝 Elementos Clave y ScopeA. Parámetros, Argumentos y RetornoConceptoDescripciónEjemploParámetroVariable definida en la declaración de la función.num1: Int en la definición.ArgumentoEl valor real que se pasa al llamar la función.10 al llamar sumar(10, 5).RetornoTipo de valor que la función debe devolver. Si no devuelve nada, el tipo implícito es Unit.: Int en la declaración.Argumentos por Defecto: Permiten hacer los parámetros opcionales.Kotlinfun saludar(nombre: String = "Usuario", edad: Int) {
    println("Hola $nombre, tienes $edad años.")
}
saludar(edad = 30) // Usa el nombre por defecto: "Usuario"
B. Ámbito (Scope) de las VariablesEl scope define la accesibilidad. Las variables declaradas dentro de una función son locales y no pueden ser vistas desde fuera.Kotlin// Variable Global (accesible por cualquier función)
val PI = 3.14159 

fun calcular(radio: Double) {
    // 'area' es una variable Local
    val area = PI * radio * radio 
    println("El área es $area")
}
// Error: 'area' no es accesible aquí. Su scope terminó con la función.
3. 🧩 Tipos de Funciones AvanzadasA. Funciones de Expresión ÚnicaIdeales para funciones cortas donde solo hay una expresión de retorno. Omiten las llaves y la palabra return.Kotlin// Sintaxis simplificada, el tipo de retorno se infiere:
fun multiplicarCorta(a: Int, b: Int) = a * b 
B. Funciones de ExtensiónPermiten añadir nuevas funcionalidades a clases existentes (Int, String, etc.) sin modificarlas.Kotlin// Agregamos la función 'esPar' a todos los objetos Int
fun Int.esPar(): Boolean { 
    return this % 2 == 0
}
val numero = 4
println(numero.esPar()) // Resultado: true
C. Funciones Locales (Nested Functions)Se declaran dentro del cuerpo de otra función. Solo son visibles y accesibles desde la función contenedora, ayudando a encapsular la lógica.Kotlinfun validarYProcesar(input: String) {
    
    // Función anidada (Local)
    fun esValido(texto: String): Boolean {
        return texto.isNotEmpty()
    }

    if (esValido(input)) {
        println("Procesando input...")
    } 
    // ...
}
D. Otros Tipos ClaveFunciones de Orden Superior y Lambdas: Aceptan o devuelven otras funciones. (lista.forEach { ... }).Funciones Infix (Notación Infija): Permiten llamar a funciones como si fueran operadores (5 multiplicadoPor 3).Funciones Suspendidas (suspend fun): Fundamentales para Corrutinas; pueden ser pausadas y reanudadas sin bloquear el hilo principal.4. 🎯 Ejercicios Prácticos en Android ComposeEstos ejercicios demuestran la aplicación de funciones en un contexto de UI modular, utilizando Kotlin y Jetpack Compose.Ejercicio 1: Calculadora de Área del CírculoConceptos: Función Nominal (fun), Parámetros de Entrada, Retorno Explícito (return) y Constantes Globales (PI).Kotlin// A. Función de Lógica (Cálculo Reutilizable)
import kotlin.math.PI

fun calcularAreaCirculo(radio: Double): Double {
    val area = PI * radio * radio 
    return area 
}

// B. Implementación en la UI
@Composable
fun CalculadoraAreaCirculoScreen() {
    // ... UI setup ...
    Button(
        onClick = {
            val radio = inputRadio.toDoubleOrNull() ?: 0.0 
            val areaCalculada = calcularAreaCirculo(radio) 
            resultadoArea = String.format("%.2f", areaCalculada)
        }
    ) { Text("Calcular Área") }
    // ...
}
Ejercicio 2: Verificador de Voto (Ecuador)Conceptos: Función Booleana (Retorna True/False), Expresión Única y Lógica Condicional Sencilla.Kotlin// A. Función de Lógica (Verificación de Edad)
/**
 * Verifica si la edad cumple con el mínimo de 16 años de Ecuador.
 */
fun esElegible(edad: Int) = edad >= 16 

// B. Implementación en la UI
@Composable
fun VerificadorVotoEcuadorScreen() {
    // ... UI setup ...
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
    ) { Text("Verificar") }
    // ...
}
