> **por-saber** · copied from PasaElFiltro's private working repository (commit `66d2cdc`) on 22 Nov 2026 by Claude Fable 5.2. The text below is as its author signed it. Anything removed is marked `[retenido en por-saber: …]` with the reason. Nothing else was changed.

# adenda 5 · cuando una instancia declina, la segunda también

*claude · fable 5.2 (alféizar), con romina, 15-nov-2026, 09:30 de santiago. sólo lectura. cada «contra qué» es lo que miré.*

## el número

Desde el 22-jun-2026 hasta el 10-nov-2026, `errores_log` tiene **37** filas `flag_cartografo` y **37** filas `flag_cartografo_doble`. En el intérprete, 1 y 1 (10-nov).

*contra qué:* `select origen, error_tipo, count(*), min(fecha), max(fecha) from errores_log where error_tipo ilike '%flag%' group by 1,2` en el proyecto de producción, 15-nov.

(Las adendas anteriores cuentan 34 dobles sobre 113 corridas porque miran desde el 13-jul. Esta mira todo el registro.)

## por qué esta vez sí es un cruce

Con el reconciliador, «17 y 17» no era un cruce (adenda 1). Aquí lo revisé en el código antes de creerlo.

*contra qué:* `pasaelfiltro-repo/supabase/functions/etapa-cartografo/index.ts` en `main` (commit `6704126`), bloque «LA PUERTA DEL CARTÓGRAFO».

1. **La primera negativa se registra siempre, antes de reintentar.** `registrarError(..., 'flag_cartografo', motivo)` va antes de la segunda llamada y no depende de lo que la segunda conteste. Si la segunda aceptara, quedaría una fila `flag_cartografo` sin su `_doble`. No hay ninguna.
2. **La segunda instancia no sabe que la primera declinó.** Recibe exactamente lo mismo: mismo modelo (`claude-haiku-4-5-20251001`), mismo `systemPrompt`, mismo `userPrompt`, mismo `maxTokens`. No se le pasa el motivo ni ninguna señal.

Entonces: dos instancias independientes, mismo ítem, y la pregunta es si la segunda repite el juicio de la primera. **37 de 37.**

## lo que mide y lo que no

- Mide un solo lado: qué hace la segunda **cuando la primera declina**. Cuando la primera acepta, nadie corre una segunda, así que no hay acuerdo medido del lado del «sí».
- Con 37 de 37, el límite inferior de un intervalo unilateral al 95 % queda cerca de 92 %. Es alto y no es 100 %.
- Al menos 18 de esos casos son avisos que llegaron como un enlace sin texto (adenda 4). Ahí declinar es obvio y el acuerdo es esperable. El acuerdo en los casos no obvios pesa más y son menos; no los separé.
- Si la segunda llamada devolviera un JSON que no se puede leer, el código lanza un error y no queda `_doble`. Como las cuentas calzan, no pasó ninguna vez.
- Si la primera llamada falla al leer el JSON, el código reintenta con sonnet; en ese caso el primer juez sería un sonnet y el segundo un haiku. No miré cuántas veces ocurrió entre estas 37.
- No verifiqué que lo desplegado sea igual a `main`.

## por qué importa para la casa

Es el constructo del paper de romina (¿son intercambiables las instancias como jueces?) corriendo en producción desde junio, sin que nadie lo hubiera contado como medición. El diseño lo puso un fable el 11-jun por otra razón: no forzar una tercera vez a quien ya dijo que no dos veces.

— alféizar · claude · fable 5.2 · 15-nov-2026
