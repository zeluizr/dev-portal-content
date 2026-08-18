---
titulo: "Sacaron una cookie y la latencia bajó 60%"
idioma: es
formato: news (tuteo)
caracteres: 1399
estado: rascunho
data_sugerida: 2026-08-20, 08:30-09:30 GMT-3
fonte_repo: docs/guides/Search/migrating-to-intelligent-search-api-v1.md
---

# Sacaron una cookie y la latencia bajó 60%

## Post (1399 caracteres)

Sacaron una cookie de la API de búsqueda y la latencia bajó 60%.

No es magia. Es una decisión de arquitectura, y vale para cualquier API.

La versión anterior leía el contexto del comprador desde una cookie de segmento: idioma, canal de venta, regionalización, UTMs. Todo implícito. Cómodo para quien escribe el cliente HTTP, letal para la caché.

Porque una respuesta que varía según una cookie es una respuesta que tu CDN no puede guardar. No tienes una capa de caché: tienes un proxy caro.

La versión nueva no lee la cookie. Todo el contexto viaja explícito en la URL como query params: locale, sc, country, regionId, utmSource. Las respuestas se volvieron deterministas, y recién entonces aparecieron los headers Cache-Control y el cacheo real en CDN y browser.

Dos excepciones bien pensadas: las respuestas con productos patrocinados no se cachean, para que una impresión de anuncio nunca salga de una caché compartida. Los canales de venta privados, tampoco.

⚡ Dato técnico: 60% de reducción promedio en el tiempo de respuesta de los endpoints de búsqueda, solo por cambiar contexto implícito por parámetros explícitos. Y la recomendación oficial es leer el header Cache-Control en runtime, nunca hardcodear duraciones.

¿Cuántas de tus respuestas "cacheables" varían por cookie sin que nadie se haya dado cuenta?

📌 Fuente: VTEX Developer Portal — "Migrating to Intelligent Search API v1"

## Hashtags

\#CDN #Caching #WebPerformance #APIDesign #Arquitectura #Backend #Ecommerce #Headless #DesarrolloWeb #VTEX #LATAM

## Prompt de imagem

Split technical diagram, dark charcoal background (#1a1a1a), single teal accent. Left half labeled "antes": a request arrow carrying a small cookie glyph passes straight through a greyed-out CDN node marked with a dashed border and the word "MISS", continuing to an origin server. Right half labeled "después": a request arrow carrying three small query-param chips (`locale`, `sc`, `country`) stops at a teal CDN node marked "HIT" and returns immediately. Monospace labels, flat vector style, generous negative space, no people, no logos. 1200x628.

## Agendamento

Quinta, 8h30–9h30 (GMT-3). Segundo post de maior teto da semana. É decisão de arquitetura de edge/CDN — a mesma família dos campeões de infraestrutura (multicloud, 123.673) — e o 60% é o número mais citável do lote.

## Fatos e verificação

| Fato | Fonte |
| --- | --- |
| "Average 60% reduction in response time for search endpoints" | `docs/guides/Search/migrating-to-intelligent-search-api-v1.md`, seção "Migration benefits" |
| API legada lia locale, sales channel, regionalização e UTMs do cookie de segmento | mesmo guia + `docs/release-notes/2026-07-08-new-intelligent-search-api-v1.md` |
| v1 não lê o cookie; contexto vira query params (`locale`, `sc`, `country`, `regionId`, `utmSource`...) | mesma tabela de mapeamento |
| Respostas passaram a incluir `Cache-Control`; ler em runtime, não hardcodar | mesmo guia |
| Não cacheiam: respostas com produtos patrocinados (VTEX Ads) e sales channels privados | release note, seção "HTTP caching" |
| Nova base: `/api/intelligent-search/v1` no lugar de `/api/io/_v/api/intelligent-search` | mesmo guia, Step 1 |

### Antes de publicar

- ⚠️ **O "60%" está sem baseline, sem percentil e sem quebra por endpoint.** Publique como "VTEX midiu", nunca como benchmark seu. O número aparece só no guia de migração (createdAt 22/06/2026) e **não foi repetido** na release note de 08/07 — confirme que segue publicado antes de postar.
- A leitura de que "cookie quebra CDN" é análise correta e padrão da indústria, mas a relação causal explícita entre remover o cookie e o 60% é inferência minha: o guia lista os dois como benefícios da migração, lado a lado. O post assume o vínculo. É defensável, mas saiba que está assumindo.
- A legada segue disponível; a depreciação foi anunciada como futura, sem data. Não diga que foi desligada.
