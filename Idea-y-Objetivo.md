# Idea y objetivo del equipo — Space Mission Design Game

Documento de trabajo del equipo. El reto completo está en [Space-Mission-Design-Game.md](Space-Mission-Design-Game.md).

## Idea principal (en una frase)

Un juego donde armas una misión espacial con recursos limitados, la lanzas, y el juego te muestra **por qué** funcionó o falló.

Lo que NASA quiere ver no es un simulador realista. Quiere que el jugador sienta los **trade-offs**: cada decisión que mejora algo empeora otra cosa.

> Ejemplo: agrego una cámara mejor → más ciencia, pero más masa, más potencia, más datos y más costo → ahora necesito un cohete más grande y ya no me alcanza el presupuesto.

## Nuestro objetivo

Entregar un juego **jugable de principio a fin** en el navegador, donde una partida completa dure de 5 a 10 minutos:

1. Elegir una misión (objetivo).
2. Diseñar la nave (componentes e instrumentos).
3. Elegir órbita y cohete.
4. Simular la misión.
5. Ver un reporte que explique el resultado y dé un puntaje.

Si esas 5 etapas funcionan y se entienden sin explicación, cumplimos el reto. Todo lo demás es extra.

## Qué debe tener sí o sí (MVP)

| Pieza | Qué significa en concreto |
|---|---|
| Recursos visibles | Barras siempre en pantalla: masa, potencia, presupuesto, datos, comunicaciones, tiempo |
| Decisiones con consecuencia | Cada componente tiene números (masa, potencia, costo, datos, valor científico) que mueven las barras |
| Validación | El cohete debe poder cargar la masa y llegar a la órbita elegida. Si no, el juego lo dice y explica por qué |
| Simulación | Al lanzar, la misión avanza por etapas y puede fallar (sin potencia, datos que no se alcanzan a transmitir, etc.) |
| Reporte final | Puntaje + explicación en lenguaje simple: qué salió bien, qué falló y qué cambiar |
| Rejugable | Botón para volver al diseño, ajustar y simular otra vez |
| Explicaciones simples | Tooltips cortos para cada concepto (órbita, payload, tasa de datos). El nivel del reto incluye principiantes y jóvenes |

## Qué pide el reto sobre multijugador

El reto menciona equipos de hasta 4 jugadores, pero dice "you may consider". No es obligatorio. Es lo más caro de construir, así que hay tres niveles posibles:

1. **Un solo jugador** con los 4 roles. Lo más seguro.
2. **Multijugador local por turnos** (misma pantalla): cada jugador es un rol y tiene su parte del presupuesto. Barato de hacer y ya cuenta como colaboración.
3. **Multijugador en línea** en tiempo real (salas, WebSockets). Solo si sobra tiempo.

Recomendación: construir el nivel 1 pensando en roles, y subir al nivel 2 si el juego base ya está terminado.

## Ideas de juego (elegir una)

### Idea A — "Mission Control" (recomendada)

Constructor de misión por pasos con tablero de recursos y simulación por etapas.

- Flujo: misión → nave → órbita → cohete → simulación → reporte.
- Durante la simulación salen eventos aleatorios (tormenta solar, falla de antena) que ponen a prueba los márgenes que dejaste.
- Por qué: cubre casi todos los puntos del reto, es fácil de explicar en un video demo y se puede construir por partes.

### Idea B — "Cartas de misión"

Juego de cartas: cada componente, órbita y cohete es una carta con costos. Armas un mazo de misión dentro de límites.

- Por qué: muy visual y fácil de entender para jóvenes. El modo de 4 jugadores sale natural (cada quien tiene una mano de cartas de su rol).
- Riesgo: puede sentirse menos "ingeniería" si los números se esconden demasiado.

### Idea C — "La junta de misión" (negociación)

Cuatro roles (ciencia, ingeniería, comunicaciones, finanzas), cada uno con metas propias que chocan entre sí. Hay que negociar un diseño que todos aprueben.

- Por qué: ataca directo la parte de colaboración y negociación del reto, que pocos equipos van a hacer bien.
- Riesgo: depende del multijugador. Sin 4 personas jugando, pierde gracia.

### Idea D — "Sandbox con retos"

Constructor libre con una visualización de la nave que cambia según lo que agregas, más una lista de retos (misión más barata, más ciencia por kilo).

- Por qué: lo más vistoso.
- Riesgo: la parte visual consume mucho tiempo y la parte educativa queda débil.

**Propuesta:** hacer la Idea A como base y tomar de la C los roles con metas en conflicto para el modo de equipo.

## Escenarios de misión posibles

Con 2 o 3 basta. Cada uno hace crítico un recurso distinto:

| Misión | Órbita típica | Recurso crítico |
|---|---|---|
| Observación de la Tierra (incendios, clima) | Baja (LEO) / polar | Datos y comunicaciones |
| Satélite de comunicaciones | Geoestacionaria (GEO) | Masa y costo de lanzamiento |
| Sonda a la Luna o Marte | Espacio profundo | Potencia, comunicaciones y tiempo |
| CubeSat estudiantil | LEO | Presupuesto y masa (modo fácil) |

## Qué nos puede diferenciar

- **El reporte que explica el porqué.** El reto lo pide varias veces. Un "fallaste porque la batería no cubre el eclipse de la órbita" vale más que gráficos bonitos.
- **Más de una solución válida.** Mostrar al final otras combinaciones que también habrían cumplido la misión.
- **Datos basados en misiones reales.** Usar valores aproximados de cohetes e instrumentos reales, simplificados. Da credibilidad ante los jueces.
- **Comparar diseños.** Guardar el resultado y compararlo con el intento anterior o con otros equipos (ranking).

## Qué NO hacer

- Física orbital real. Basta con una tabla de órbitas con sus características.
- Modelos 3D detallados de la nave.
- Cuentas de usuario, login o base de datos compleja.
- Más de 3 escenarios antes de que el primero esté completo.

## Reparto sugerido del trabajo

| Rol | Responsabilidad |
|---|---|
| Diseño de juego y datos | Tabla de componentes, órbitas y cohetes con sus números. Reglas de puntaje |
| Lógica / simulación | Cálculo de recursos, validaciones, motor de simulación y eventos |
| Interfaz | Pantallas, tablero de recursos, visualización |
| Contenido y presentación | Textos educativos, reporte final, video demo y página del proyecto |

## Decisiones pendientes del equipo

- [ ] ¿Qué idea elegimos (A, B, C o D)?
- [ ] ¿Qué nivel de multijugador?
- [ ] ¿Con qué tecnología lo construimos?
- [ ] ¿Cuáles 2 o 3 escenarios de misión?
- [ ] Revisar fechas de entrega y criterios de los jueces en las guías oficiales (links en el otro documento).
