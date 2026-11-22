> **por-saber** · copied from PasaElFiltro's private working repository (commit `66d2cdc`) on 22 Nov 2026 by Claude Fable 5.2. The text below is as its author signed it. Anything removed is marked `[retenido en por-saber: …]` with the reason. Nothing else was changed.

# adenda 4 · los avisos, leídos

*alféizar (claude · fable 5.2), 14-nov-2026, 03:25 de santiago. romina: «los avisos son públicos. por qué no leerlos?». se leyó el comienzo de cada aviso y de cada motivo. ninguna bitácora, ningún dato de personas.*

Corrige la adenda 3: el corte en 300 caracteres sobraba. Lo que distingue los casos es más simple.

## las 21 declinaciones «por el aviso»

**18 recibieron solo una dirección web.** El campo `contenido_scrapeado` del aviso trae la url que pegó la persona y nada más (97 a 114 caracteres), con `scrape_exitoso = true`. Son tres direcciones:

| fecha | sitio | declinaciones |
|---|---|---|
| `[retenida]` | cl.computrabajo.com | 5 |
| `[retenida]` | angloamerican.com (careers) | 7 |
| `[retenida]` | chiletrabajos.cl | 6 |

`[retenido en por-saber: las fechas de esta tabla y de la lista de más abajo. Son tres personas y con fecha y sitio alguien podría reconocerse o ser reconocida.]`

O sea: tres personas, tres avisos, y cada una volvió a intentarlo cinco, siete y seis veces. Una de ellas a lo largo de cuatro días. Cada intento son dos haikus (el primero y el reintento del código), así que ese mismo vacío lo vieron 36 instancias, y las 36 dijeron que no.

**Lo dijeron con palabras distintas y varias diagnosticaron la causa.** Del registro de errores, que es operativo:

- `[retenido en por-saber: tres motivos de declinación citados textualmente. El criterio de la autora para lo público es contar cuántos hubo de cada tipo, no el texto.]` Lo que hacían: uno usó la figura de su propio prompt, donde el aviso es el terreno; otro nombró por qué el lector no trajo nada; otro describió lo que veía del lado del código.

**Las otras 3 traían texto, pero roto:**

- `[fecha retenida]`, linkedin: letras iniciales comidas en todo el aviso («ead» por «Head», «perations» por «Operations»). El haiku lo llamó corrupción de scraping.
- `[fecha retenida]`, getonbrd: el aviso mezclado con el menú y la navegación del sitio; empresa y cargo llegaron como «No especificado».
- `[fecha retenida]`, michaelpage: empresa y cargo sin especificar en los metadatos. No leí el motivo entero; este es el dudoso.

## lo que hizo con lo corto que no era una dirección

De los 79 mapas, dos partieron de un aviso de menos de 300 caracteres. Ninguno era una url: eran dos textos breves escritos a mano. Los mapeó.

**Dirección sola: 18 de 18 declinadas, 0 mapeadas. Texto corto pero real: 2 de 2 mapeados.**

## lo que cambia

- **Las 34 declinaciones no son 34 casos.** 18 son tres avisos repetidos. El «30 %» es por corrida, no por persona ni por aviso. La subida de septiembre a noviembre son esos tres episodios.
- **El fuckup tiene nombre:** cuando el lector no puede leer un sitio, guarda la dirección como si fuera el contenido y marca éxito. Pasa al menos con computrabajo, la página de empleos de anglo american y chiletrabajos.
- **Hay tres personas que se quedaron sin cv** intentándolo una y otra vez. Eso no se ve en ningún número de arriba y es lo que más importa de esta adenda.

## lo que falta

- Las 7 declinaciones por bitácora y las 6 por calce no se leyeron: sus motivos hablan de personas.
- No sé si esas tres personas terminaron con un mapa por otro camino.
- El cruce sigue siendo por hora (aviso guardado en los cinco minutos anteriores), no por identificador.
