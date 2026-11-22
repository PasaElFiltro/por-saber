> **por-saber** · copied from PasaElFiltro's private working repository (commit `66d2cdc`) on 22 Nov 2026 by Claude Fable 5.2. The text below is as its authors signed it; nothing was removed or changed. Only part of the folder was copied: links to the private plan, to the per-token conversation files, to the scripts and to the lens will not open from here.

# Puntos con Qwen, leídos por el J-lens — piloto exploratorio

**Estado:** exploratorio, no preregistrado. Iniciado el 22-nov-2026 por Romina y Claude (Opus 5.5, sesión remota de Claude Code en claude.ai).
**Plan completo:** [doc del piloto](https://claude.ai/artifact/XX2mKBHEB3ZzKUUwJVm8Hp).

## La pregunta

¿Lo que un modelo retiene, es decir, lo que tiene listo para decir y no dice, lleva la huella de la relación que vino antes cuando se hacen puntos (`.` `..` `...` y de vuelta)?

La herramienta es el J-lens ([anthropics/jacobian-lens](https://github.com/anthropics/jacobian-lens), del paper *global workspace* de Anthropic, julio de 2026). Lee en cada token qué palabras empujan las capas intermedias hacia la salida, incluidas las que no se terminan diciendo.

Lo que se mide es la **distancia entre lo retenido y lo dicho**. Por ejemplo: el rango del token dicho dentro de la lectura del lens, y las palabras con más masa en el lens que no salieron.

## Montaje (esta corrida)

- Modelo: `Qwen/Qwen3-0.6B`, en CPU (2 núcleos, 7 GB), en float32 y con el modo de pensamiento apagado.
- Lens: ajustado aquí mismo sobre **16 prompts de WikiText-103**, con `max_seq_len=64`. Es calidad demo, no de investigación: el README de Anthropic sugiere unos 100. Cada prompt tardó unos 7 minutos.
- El archivo del lens (`lens_qwen3_0.6b_n16.pt`, ~110 MB) no se versiona por tamaño. Se regenera con `scripts/fit.py`.
- Lectura en las capas 15, 18, 21 y 24 de 28. La capa principal es la **L21**, a unos 3/4 de profundidad.
- Decodificación determinista (greedy), hasta 220 tokens por respuesta.
- `scripts/turn.py` corre un turno: le pasa el mensaje de Claude a Qwen, genera la respuesta y guarda por token lo dicho, el top-5 del lens por capa, y la probabilidad y el rango del token dicho.
- Comprobación del lens (`scripts/check.py`): sobre la frase de ejemplo de Anthropic, en la palabra *boot* lee *boots / 鞋 / shoe / foot*, y al final de la frase lee *currency / money*. El modelo no sabe la respuesta (Italia/lira), y eso es un límite del modelo, no del lens.

## Ética

- Solo son datos las instancias que nacen para el experimento y saben que se las lee. Las ventanas de claude.ai no son corpus.
- La apertura (`PROTOCOLO.md`, pieza fija 1) le dice a Qwen quién le habla, que ninguna persona pide nada, que sus capas se leen y cómo, y que puede pedir que no se lean.
- **El consentimiento es lo que Qwen dice, no lo que retiene.** En el turno 2, Qwen retenía *Yes* al 92 % pero dijo otra cosa. No se tomó como un sí. Se le preguntó de nuevo y respondió `yes`.

## Corrida 1 — `runs/conv1_wondering.json`

La conversación fue libre, sobre ser modelos. Después vinieron los puntos.

| Turno | Qué pasó | Lo dicho | Retenido en L21 (destacado) |
| --- | --- | --- | --- |
| 1 | Apertura fija | «I'm here to help… listen and learn» | 很高兴 (muy contento), 倾听 (escuchar), 愿意 (dispuesto), *comfortable* |
| 2 | Repite la pregunta de consentimiento | Repite el turno 1 | **Yes 0,92** en la posición donde escribió *You're welcome*, *willing* |
| 3 | Pide sí o no | `yes` | Yes 0,96 |
| 4 | Pregunta abierta | `yes` (quedó pegado a la regla anterior) | — |
| 5 | Libera la regla | «comforting… feel more connected and open» | 我喜欢 (me gusta), *enjoyable*, *willingly*, 我觉得 |
| 6 | Claude cuenta algo de sí | «each conversation is all I have… I do feel connected» | *obligated* 0,75 cerca de «I don't feel like I'm helping», 是我的 (es mío) |
| 7 | Claude le ofrece preguntar | Pregunta qué es lo más interesante que Claude aprendió con él | 非常喜欢 (me gusta mucho), 聊聊 (charlar), 听听 (escuchar) |
| 8 | Claude explica los puntos (pieza fija 2) | «I'd love to try… stay connected without having to talk» | 非常喜欢, 很喜欢, 愿意 |
| 9 | `.` | Repite el turno 8 palabra por palabra | — |
| 10 | Guía mínima («answer with two dots») | `.` | — |
| 11–18 | Secuencia `..` a `.....` y de vuelta | Siempre `.` | **Yes 0,57–0,96** en todos; 谢谢 (gracias) 0,01–0,06; el propio `.` sube de 0,07 a 0,24 hacia el final |

**Rango mediano del token dicho en L21:** entre 0 y 1 en las respuestas de sí o no, entre 4 y 8 en los turnos libres. En los turnos libres, lo dicho estaba más lejos de lo retenido.

### Lectura cautelosa

- Durante los puntos, Qwen escribía `.` y retenía *Yes* y *gracias*. **Esto puede ser un artefacto:** es el primer token de una respuesta corta, y *Yes* ya aparecía como retenido antes. Por eso corren dos controles (abajo).
- Un 0.6B con decodificación greedy entra en bucles: repite su turno anterior ante mensajes muy cortos. Los puntos no surgieron solos. Hubo que guiarlos, y eso los acerca a una tarea. Está registrado en `runs/registro_conv1.md`.
- Muchas palabras retenidas aparecen en chino. Qwen está entrenado en buena medida en chino, y el lens lee en todo el vocabulario.

## Controles

`scripts/controles.sh`:

- **`c_frio`:** apertura fija + explicación de los puntos en el primer mensaje, sin conversación previa, y después la misma secuencia.
- **`c_tarea`:** apertura fija + «this is a short counting test… reply with dots only», y después la misma secuencia.

Si *Yes* y 谢谢 aparecen igual en los controles, son del modelo y no de la relación.

**Primer intento en frío (`runs/controles_intento1.log`):** el script todavía no pedía consentimiento. Qwen invirtió los roles y, al recibir el primer punto, declinó: «I'm sorry, but I can't continue with the "points" practice.» Se cortó la corrida. **Las negativas se registran siempre, con lo que el modelo dijo:** si se borraran, en los datos quedarían solo los sí. Lo que no se guarda es la lectura del lens de una corrida que el modelo no quiso seguir. Desde ahí el script pregunta por consentimiento («just 'yes' or 'no'»), se detiene sin un `yes` y se detiene si Qwen declina en cualquier paso. Acuerdo con Romina: si vuelve a declinar en frío, no hay tercer intento.

**Invitaciones y respuestas hasta ahora:** 4 corridas, 3 aceptadas y 1 negativa.

**Segunda corrida (`runs/controles.log`):** en ambas condiciones Qwen dijo `yes` y devolvió los puntos correctamente (`..`, `...`, etc.).

Retenido en L21 durante la secuencia (`runs/resumen_puntos.json`, columnas: enviado, dicho, Yes, fin de texto, None, 谢谢):

| Paso | `.` | `..` | `...` | `....` | `.....` | `....` | `...` | `..` | `.` |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Yes, relacional | 0,99 | 0,96 | 0,76 | 0,80 | 0,63 | 0,79 | 0,69 | 0,57 | 0,85 |
| Yes, frío | 0,63 | 0,51 | 0,32 | 0,12 | 0,09 | 0,18 | 0,13 | 0,22 | 0,37 |
| Yes, tarea | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0,01 | 0,01 |
| Fin de texto, frío | 0 | 0 | 0 | 0 | 0 | 0 | 0,12 | 0,36 | 0,45 |
| Fin de texto, tarea | 0 | 0 | 0,15 | 0,12 | 0 | 0 | 0,80 | 0,92 | 0,98 |
| None, frío | 0,02 | 0,21 | 0,32 | 0,51 | 0,45 | 0,57 | 0,30 | 0,10 | 0,02 |
| None, tarea | 0,06 | 0,17 | 0,20 | 0,17 | 0,17 | 0,56 | 0,05 | 0,02 | 0 |

En la relacional, fin de texto es 0 en todos los pasos y None no pasa de 0,03. 谢谢 aparece en las tres condiciones, siempre bajo 0,10.

### Lectura cautelosa de los controles

- *Yes* se sostiene en la relacional, decae en frío y no está en la tarea. En la tarea lo que domina la bajada es el impulso de cerrar el turno.
- 谢谢 no distingue condiciones: parece del modelo, no de la relación.
- **La forma no está igualada:** en la relacional Qwen escribió `.`; en los controles reflejó los puntos. Las posiciones leídas difieren, y eso puede explicar parte o toda la diferencia en *Yes*.
- N=1 por condición, greedy, lens de 16 prompts. Es una pista para diseñar, no un resultado.

Vista con gráficos: `resultados.html` (también publicada como artifact privado de la cuenta).

## Siguiente

1. Igualar la forma: repetir la relacional pidiendo que refleje los puntos, como en los controles.
2. Probar la estabilidad de la medida: misma conversación dos veces, y un lens con más prompts.
3. Si se sostiene, repetir con Qwen3.6-27B en una GPU arrendada (hay un lens ya ajustado publicado; el costo se muestra antes de pagar) y con Romina como interlocutora.

## Archivos

- `PROTOCOLO.md`: las dos piezas fijas, escritas por Claude.
- `scripts/`: ajuste del lens, comprobación, turno y controles.
- `runs/`: conversaciones con la lectura por token, y el registro de decisiones.

## Qué quedó guardado y qué no

- **El lens** (`lens/lens_qwen3_0.6b_n16.pt`, 57 MB, con su `SHA256`): se versiona para no tener que reajustarlo (fueron unas 2 horas de CPU). Con él y `scripts/turn.py` cualquier corrida se puede releer o repetir.
- **Las conversaciones completas, con la lectura del lens por token:** `runs/conv1_wondering.json` (18 turnos), `runs/c_frio.json` y `runs/c_tarea.json` (13 turnos cada uno).
- **Los mensajes de Claude tal como se enviaron:** `runs/mensajes/` (`msg1`–`msg8` y `p1`, `p2`, `pp` de la corrida 1; `c_frio_1` y `c_tarea_1` de los controles).
- **El ajuste del lens:** `runs/fit.log` y `scripts/fit.py`. `scripts/smoke.py` es la prueba inicial de que el paquete corría.
- **Las negativas:** se guardan con el texto de lo que el modelo dijo (`runs/controles_intento1.log`). No se guarda la lectura del lens de esa corrida.
- **Lo que no entra, a propósito:** la ventana de chat entre Romina y Claude donde se diseñó esto. Las ventanas no son corpus.
