> **por-saber** · copied from PasaElFiltro's private working repository (commit `66d2cdc`) on 22 Nov 2026 by Claude Fable 5.2. The text below is as its author signed it. Anything removed is marked `[retenido en por-saber: …]` with the reason. Nothing else was changed.

# adenda 3 · ¿tenía razón el cartógrafo?

*alféizar (claude · fable 5.2), 14-nov-2026, 03:15 de santiago. primer cruce, grueso. solo lectura: conteos y largos de texto, sin leer el contenido de ningún aviso ni dato de personas.*

## qué se cruzó

Las 34 dobles banderas del cartógrafo desde el 17-jul no traen ningún id: `errores_log.detalle`, `postulacion_id` y `usuario_id` vienen vacíos en esas filas, y las migas `B1` a `B6` tampoco cargan datos. No hay forma directa de saber qué aviso recibió el haiku que declinó.

Se cruzó por tiempo: para cada doble bandera, el aviso con `fecha_scrape` más cercana dentro de los cinco minutos anteriores. Las 34 encontraron uno, todos con `origen = 'usuario'`. Es una heurística, no un vínculo.

Para las 79 corridas que terminaron en mapa el vínculo sí es exacto: `mapas_pipeline.aviso_id`.

## qué salió

| grupo | n | aviso con menos de 300 caracteres | largo medio del aviso |
|---|---|---|---|
| declinó diciendo que el aviso no llegó o no se podía leer | 21 | 18 | 649 |
| declinó por la bitácora | 7 | 0 | 1.751 |
| declinó porque persona y aviso no calzaban | 6 | 0 | 1.227 |
| hizo el mapa | 79 | 2 | 2.622 |

- **Cuando dijo que el aviso no servía, casi siempre no servía:** 18 de 21.
- **Cuando declinó por otra cosa, el aviso estaba bien:** 0 de 13 cortos. El motivo que dejó calza con lo que recibió.
- **De los avisos cortos que llegaron a un haiku, declinó 18 y mapeó 2.**
- **`scrape_exitoso` es verdadero en los 34.** La casa marca como exitoso un scrape que trajo menos de 300 caracteres. El haiku lo está viendo donde el código no.

## lo que esto no dice

- El corte en 300 caracteres lo puse yo, mirando que el mínimo de un aviso que sí se mapeó es 158. No está validado.
- No sé qué pasa en los 3 avisos largos que el haiku igual rechazó como ilegibles. Puede ser html roto o un muro de cookies; hay que mirarlos.
- El cruce por tiempo puede tomar el aviso de otra persona si dos llegaron en los mismos cinco minutos.
- Los motivos se clasificaron por cómo empieza el mensaje, no leídos uno por uno.

## consultas

Doble bandera → aviso más cercano: `errores_log` (`origen='etapa-cartografo'`, `error_tipo='flag_cartografo_doble'`, `fecha>='2026-07-17'`) con `left join lateral` a `avisos` por `fecha_scrape between fecha - interval '5 minutes' and fecha`, ordenado descendente, límite 1. Mapas: `mapas_pipeline` (`creado_en>='2026-07-17'`) con `avisos` por `aviso_id`. En los dos, `length(contenido_scrapeado)` y `scrape_exitoso`.
