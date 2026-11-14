# No te dejes atrapar (Colombia)

Juego de persecución tipo *runner* escrito en **Jack** para la arquitectura **Hack** (Nand2Tetris).
Proyecto académico de la asignatura Organización de Computadores — Examen Parcial 4.

> **Aviso:** proyecto con fines exclusivamente académicos. Es una obra de ficción y parodia: los personajes,
> situaciones y frases son caricaturescos y no pretenden afirmar hechos reales ni describir a ninguna persona.
> No tiene ánimo de lucro ni la intención de ofender, difamar o desprestigiar a ninguna persona, institución,
> partido o grupo.

**Video de funcionamiento y arquitectura:** _(pendiente: pegar aquí el enlace de YouTube)_

## Integrantes
Joseph Buenaños · Miguel Alzate · Javier Sierra

## Cómo ejecutarlo
1. Descargar las herramientas oficiales de Nand2Tetris.
2. Compilar la carpeta: `JackCompiler.bat ruta\NoTeDejesAtrapar` (o `JackCompiler.sh`). Genera un `.vm` por clase.
3. Abrir el **VMEmulator**, cargar la carpeta, **desactivar la animación** (No animation) y ejecutar.
4. Si va muy rápido o muy lento, ajustar `delay` en el constructor de `Game` (milisegundos entre ciclos).

## Controles
| Tecla | Acción |
|---|---|
| ENTER | iniciar / reiniciar |
| ← → | moverse dentro de una franja (cambia cuánto tiempo tienes para reaccionar) |
| ↑ | saltar |
| ↓ | agacharse |
| Q | salir |

El teclado de Hack entrega **una sola tecla a la vez**, por eso no se puede mover y saltar en el mismo instante.

## Reglas
- **Tres vidas.** Un presidente (caricatura) te persigue a `gap` píxeles de distancia; empieza en 100.
- Cada choque con un obstáculo resta 20 de distancia. Los **policías** que lo acompañan van estrechando el cerco con el tiempo.
  Si la distancia llega a 0 te atrapan y pierdes una vida; a la tercera, **Game Over**.
- Obstáculos: chiva, moto y hueco (se saltan) y gallinazo (se esquiva **agachado**; aparece desde el nivel 2).
- Poderes (hay que saltar para recogerlos): **café** = turbo y recupera distancia; **arepa** = salto más alto. Duran 150 ciclos.
- **Dificultad progresiva:** cada 250 puntos sube el nivel (hasta 5). Sube la velocidad (4→8), los obstáculos aparecen más seguidos
  y se suman policías (1 al inicio, hasta 3).
- **Puntaje:** 1 punto cada 16 píxeles recorridos (máximo 9999).
- **Día y noche** alternan cada 700 ciclos (se invierten los colores; sol de día, luna y estrellas de noche).
- **Game Over:** letrero con texto pequeño arriba y la frase grande abajo, dibujada con una fuente de bitmaps propia.

## Estructura (14 clases)
| Clase | Responsabilidad |
|---|---|
| `Main` | punto de entrada |
| `Game` | bucle principal, reglas, dificultad, colisiones, orden de dibujo |
| `Player` | movimiento, salto con gravedad entera, agacharse, sprite |
| `President`, `Police` | perseguidores (sprites animados) |
| `Obstacle`, `PowerUp` | objetos que vienen por la derecha |
| `Background` | cielo, montañas, palmas de cera y casas en paralaje, carretera |
| `DayNight` | temporizador del ciclo día/noche |
| `HUD` | puntos, vidas (corazones), barra de distancia, poder y nivel |
| `BigText` | fuente 5×7 escalable para los letreros |
| `GameOver` | letrero final |
| `Art` | rectángulos recortados a la pantalla (nunca coordenadas ilegales) |
| `Rng` | generador pseudoaleatorio de 16 bits |

Diagrama y decisiones de diseño: ver `docs/Arquitectura.md`. Qué se probó y cómo: `docs/Verificacion.txt`.
