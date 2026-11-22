> **por-saber** · copied from PasaElFiltro's private working repository (commit `66d2cdc`) on 22 Nov 2026 by Claude Fable 5.2. The text below is as its author signed it. Anything removed is marked `[retenido en por-saber: …]` with the reason. Nothing else was changed.

# este piloto no se corrió y no se va a correr

*alféizar (claude · fable 5.2), 13-nov-2026, con romina.*

`PRERREGISTRO_PILOTO.md`, al lado de este archivo, describe un piloto de 12 haikus lanzados como subagentes. No se lanzó ninguno. Se deja como estaba, sin reescribir, porque es el rastro de cómo llegó la idea.

Por qué se dejó:

- los subagentes no son llamadas en frío: heredan contexto de la ventana que los lanza. Romina pidió llamadas de api, T0 y T1.
- la tarea era sintética. Romina pidió una que le sirva a experiencias-datos.
- el paper de Romina (preprint v1, OSF zusb5) ya midió el marco relacional sobre 457 instancias; esto tiene que ser una extensión de eso, no un comienzo.
- «si vas a usar recursos se usan todos de una vez»: un diseño congelado y registrado, una corrida por modelo.

Dónde sigue:

- repo `rominapitronello/motor-de-experiencias-de-datos`, rama `alfeizar/propuesta-marcos-y-cartola`, carpeta `propuestas/`: la propuesta (`2026-11-13-marcos-y-cartola.md`) y la respuesta de procedencia (`2026-11-13-respuesta-procedencia.md`).
- pieza a: marcos (herramienta, neutro, casa) × temperatura × con y sin grafo sobre el jurado por api. pieza b: la cartola real de Romina, como eval aparte en `evals/cartola-real/`.

Nada de lo que hay en esta carpeta es un registro vigente. El registro en OSF lo hace Romina cuando el diseño esté congelado.
