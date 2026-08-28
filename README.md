EJERCICIO 1: LENGUAJE CONSIDERADO:C.

Generalización simbólica (reglas escritas del lenguaje)
Son las reglas formales, la sintaxis y semántica que definen qué es un programa válido en C:

Tipado estático y explícito: toda variable debe declararse con un tipo antes de usarse (int x;, char c;, float f;), y el compilador verifica esos tipos en tiempo de compilación. Estructura de bloques: el código se organiza con llaves { }, cada instrucción termina en ;. Funciones como unidad principal: todo programa arranca en main(), y se organiza en funciones que reciben parámetros por valor. Gestión manual de memoria: reglas explícitas para reservar (malloc) y liberar (free) memoria; el lenguaje no gestiona esto automáticamente. Aritmética de punteros: reglas formales sobre cómo los punteros pueden sumarse, restarse y desreferenciarse (*, &). Compilación en etapas: preprocesador (macros, #include), compilación y enlazado (linking) como pasos separados y bien definidos.

Estas reglas están formalizadas en el estándar ANSI C / ISO C, que es literalmente el documento normativo del lenguaje.

Creencias de los profesionales (qué se cree "mejor" que en otros lenguajes)
Entre programadores de C, suele haber consenso en que:

Es más rápido y eficiente que lenguajes de alto nivel, porque compila directo a código máquina sin capas intermedias (sin máquina virtual, sin garbage collector). Da control total sobre la memoria y el hardware, algo que lenguajes como Python o Java deliberadamente ocultan. Es más "honesto" sobre lo que hace la computadora: no hay magia oculta, cada línea tiene una traducción casi directa a instrucciones de bajo nivel. Es portable: un mismo código C compila en distintas arquitecturas con cambios mínimos, lo que se considera superior a escribir en ensamblador específico de cada procesador.

Estilo imperativo como filosofía central: Ritchie y Thompson diseñaron C bajo el paradigma imperativo, donde el programador describe paso a paso la secuencia exacta de operaciones que debe ejecutar la computadora (asignaciones, bucles, condicionales, control de flujo explícito), en contraposición a estilos declarativos donde solo se describe el resultado deseado. Esto refleja el valor de darle al programador control explícito sobre el "cómo", en lugar de delegar esas decisiones a un motor de más alto nivel — coherente con la cercanía al hardware que buscaban.

Ejemplares (qué problemas resuelve mejor este lenguaje)

C se destaca particularmente en:

Sistemas operativos: Unix, Linux y buena parte de Windows están escritos en C. Programación de sistemas embebidos: microcontroladores, firmware de electrodomésticos, IoT, donde los recursos (memoria, CPU) son muy limitados. Drivers y controladores de hardware: necesitan acceso directo a memoria y registros del procesador. Desarrollo de otros lenguajes/intérpretes: muchos lenguajes (Python, PHP, Ruby) tienen su intérprete principal escrito en C. Software de alto rendimiento: motores de bases de datos, compiladores, sistemas donde cada milisegundo importa.

No es ideal, en cambio, para desarrollo web rápido, aplicaciones con mucha lógica de negocio donde la velocidad de desarrollo importa más que la eficiencia, o proyectos donde el equipo prioriza seguridad automática sobre control manual.

EJERCICIO 2: LENGUAJE CONSIDERADO : C

C tiene una sintaxis formalmente especificada mediante gramáticas (notación BNF/EBNF) y su semántica está definida en estándares oficiales:
ANSI C (C89/C90): primera estandarización formal (1989) ISO/IEC 9899: estándar internacional, con revisiones sucesivas: C99, C11, C17, C23

Estos documentos definen con precisión la sintaxis (qué es un programa válido) y la semántica (qué significa cada construcción, qué comportamiento tiene). Aun así, C tiene zonas de "comportamiento indefinido" (undefined behavior) deliberadamente dejadas abiertas por el estándar (por ejemplo, desbordamiento de enteros con signo, acceso fuera de los límites de un array), lo cual es una particularidad importante del lenguaje.

¿Es posible comprobar el código producido en ese lenguaje?
Parcialmente. C permite cierta verificación, pero con limitaciones:

El compilador detecta errores de sintaxis y algunos errores de tipos (aunque el sistema de tipos de C es relativamente débil comparado con lenguajes como Haskell o Rust). Existen herramientas externas de análisis estático (Valgrind, Clang Static Analyzer, cppcheck) para detectar fugas de memoria, punteros inválidos, etc., pero no son parte del lenguaje en sí. No hay verificación automática de límites de arrays, ni de punteros nulos, ni gestión segura de memoria en tiempo de compilación — esto queda 100% en manos del programador, lo que hace que muchos errores solo aparezcan en tiempo de ejecución (o ni siquiera ahí, si el comportamiento es indefinido).

En resumen: es comprobable a nivel sintáctico, pero débilmente verificable a nivel semántico/seguridad.

¿Es confiable?
Depende del criterio con el que se mida:

Confiabilidad de ejecución/rendimiento: sí, muy alta — es predecible, sin sorpresas de un recolector de basura pausando el programa, sin capas ocultas. Confiabilidad frente a errores del programador: baja — C no protege contra errores comunes como desbordamiento de buffer, punteros colgantes (dangling pointers), fugas de memoria o null pointer dereference. Esto históricamente causó muchísimas vulnerabilidades de seguridad (buffer overflows, por ejemplo).

Se podría decir que C es confiable en su comportamiento (hace exactamente lo que el estándar dice, sin magia oculta) pero poco confiable en cuanto a prevenir errores del desarrollador.

¿Es ortogonal?
Medianamente. La ortogonalidad significa que las construcciones del lenguaje pueden combinarse libremente sin restricciones ni casos especiales.

C tiene bastante ortogonalidad en ciertos aspectos: los punteros pueden apuntar a casi cualquier tipo, las estructuras de control (if, for, while) son combinables libremente, las funciones pueden recibir y devolver casi cualquier tipo. Pero también tiene excepciones no ortogonales: los arrays no son verdaderos objetos de primera clase (no se pueden asignar directamente uno a otro con =), las funciones no pueden anidarse ni tratarse completamente como valores (no hay funciones de primera clase reales, aunque sí punteros a función), y hay reglas especiales para cadenas de caracteres (arrays de char terminados en \0) que no siguen las reglas generales de otros tipos.

Características de consistencia y uniformidad C es bastante consistente en su sintaxis básica: la forma de declarar variables, condicionales y bucles sigue un patrón repetido y predecible en todo el lenguaje. Sin embargo, tiene inconsistencias históricas conocidas: por ejemplo, la precedencia de operadores tiene casos poco intuitivos (& y | bit a bit tienen menor precedencia que ==, lo cual genera errores comunes), y la sintaxis de declaración de punteros a funciones es notoriamente confusa y poco uniforme respecto al resto del lenguaje. La biblioteca estándar también es más una colección de funciones agregadas con el tiempo que un diseño totalmente uniforme desde el inicio.

¿Es extensible? ¿Hay subconjuntos del lenguaje? Extensible: sí, principalmente a través de bibliotecas (no cambiando el lenguaje en sí). El núcleo del lenguaje es deliberadamente pequeño, y toda funcionalidad extra (E/S, manejo de strings, matemáticas) se agrega vía bibliotecas externas (stdio.h, string.h, math.h, etc.). También permite macros con el preprocesador (#define) para extender la sintaxis de forma limitada. Subconjuntos: sí, existen. Por ejemplo: MISRA C: subconjunto restringido usado en sistemas críticos (automotriz, aeroespacial) que prohíbe construcciones peligrosas del lenguaje. C embebido / Embedded C: subconjuntos usados en microcontroladores con recursos limitados. Distintos compiladores implementan distintos subconjuntos/extensiones (GNU C con extensiones de GCC, por ejemplo).

El código producido, ¿es transportable (portable)?

Sí, en un grado alto — es una de las mayores fortalezas históricas de C:

El código C bien escrito según el estándar puede compilarse en distintas arquitecturas y sistemas operativos con cambios mínimos o nulos, gracias a que existen compiladores de C para prácticamente cualquier plataforma (desde microcontroladores hasta supercomputadoras). Esta portabilidad fue justamente el motivo por el que Unix se reescribió en C en los años 70: permitió portar el sistema operativo a distintas arquitecturas de hardware sin reescribirlo en ensamblador para cada una. Limitación: el código puede volverse no portable si depende de detalles específicos de implementación (tamaño exacto de tipos como int, orden de bytes/endianness, extensiones específicas de un compilador como GCC), por eso el estándar deja varios de estos aspectos como implementation-defined en vez de fijarlos rígidamente.
