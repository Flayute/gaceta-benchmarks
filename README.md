# La Gaceta del LLM — benchmarks

Datos crudos de las pruebas de [La Gaceta del LLM](https://gacetallm.netlify.app/):
modelos de lenguaje en hardware discreto. Producción 100 % automatizada
(recopilación Hugging Face → benchmark propio → redacción por LLM local),
con dirección editorial humana y revisión antes de publicar.

## Cómo se mide (receta)

- **Hardware flayute**: RX 7900 XT 20 GB (ROCm0) · RX 7900 GRE 16 GB (ROCm1) · 64 GB RAM.
- **Hardware remota**: gpu-rtx-remota RTX 3050 8 GB (CUDA).
- **Motor**: llama.cpp (fork mtp, build b5517, ROCm; fork CUDA en la rtx).
- **Velocidad (tg)**: `llama-bench -pg 512,128 -r 2 -fa auto -dev <GPU>` — NUNCA HTTP sin chat template.
- **Contexto máximo**: ladder 8k→256k con KV f16 y q8_0, `-ngl auto`, KV-offload default.
- **Estabilidad**: 12 peticiones encadenadas con contexto creciente; se registran cuelgues y degradación.
- Los resultados negativos y descartados se publican también (campo `negativo`, `incidencias`): un fallo medido es conocimiento.

## Contenido

- `experiments/index.jsonl` — registro con ID `EXP-<fecha>-<TIPO>-<nnn>` (CTX, SUITE, BENCH, AGENT, CAL, STAB).
- `raw/<corrida>/…json` — JSONs originales de cada corrida (saneados).
- `revistas/` — archivo de números publicados: `numero-N/index.html` es la revista completa
  (portada, editorial, artículos, laboratorio y comunidad) y `revistas/index.json` el índice del archivo.
- `raw/x_reactions_*/x_posts.json` — vaciado de posts de X citados en los números, con @handle, fecha y URL
  de cada status. Los posts citados se reproducen brevemente con atribución; el texto íntegro queda en el JSON.
  Las cifras de engagement (me gusta, retweets) no están: el buscador usado no las devuelve.

Licencia: CC BY 4.0 — cita "La Gaceta del LLM" si reutilizas los datos.
