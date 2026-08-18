---
titulo: "100 requests por minuto, anunciados después"
idioma: es
formato: news (tuteo)
caracteres: 1289
estado: rascunho
data_sugerida: 2026-08-17, 12:00-13:00 GMT-3
fonte_repo: docs/release-notes/2026-08-04-vtex-ads-api-reports-rate-limit.md
---

# 100 requests por minuto, anunciados después

## Post (1289 caracteres)

100 requests por minuto por cuenta.

Ese es el nuevo límite en los endpoints de Reports de la API de VTEX Ads. Si te pasas, recibes un 429 con el mensaje "Rate limit exceeded for this account". Aplica solo a llamadas con API Key: el uso desde la interfaz no se toca.

Lo interesante no es el número. Es el orden de los factores.

El límite llegó después de que las integraciones ya estaban en producción. Y el que más lo sufre es justamente el que construyó el pipeline más completo: cargas históricas, syncs diarios totales, todo lo que dispara muchas requests seguidas precisamente porque alguien pidió datos confiables.

Un límite anunciado sobre integraciones que ya corren no es un límite. Es un breaking change con mejor nombre.

La recomendación oficial es distribuir la carga en el tiempo y esperar la próxima ventana antes de reintentar. Traducido: si tu exportador no tiene backoff, ya lo necesitas. Y conviene que sea conservador por diseño, no solo reactivo.

⚡ Dato técnico: 100 req/min por cuenta, solo para llamadas con API Key. Arriba de eso, 429 con el mensaje "Rate limit exceeded for this account".

¿Tus integraciones tienen backoff, o descubres los límites del proveedor en producción?

📌 Fuente: VTEX Developer Portal — "VTEX Ads API: Rate limit on Reports endpoints"

## Hashtags

\#APIDesign #RateLimiting #Integraciones #Backend #DataEngineering #Resiliencia #Ecommerce #RetailTech #DesarrolloWeb #VTEX #LATAM

## Prompt de imagem

Minimalist chart on dark charcoal background (#1a1a1a), single orange accent. A simple step plot: a flat horizontal threshold line labeled in monospace "100 req/min", with a request-volume bar series rising underneath and the bars that cross the line rendered in orange and stamped with a small "429" tag. X axis labeled "carga histórica", no numeric ticks. Below, small monospace caption: "el límite llegó después que el pipeline". Flat vector, generous negative space, no people, no logos. 1200x628.

## Agendamento

Segunda, meio-dia (GMT-3). Segunda é slot de competição alta e este é o post de menor teto do lote — combinação certa. Serve de aquecimento para a semana sem gastar um dia bom. Se a semana estiver cheia, é o primeiro a cortar.

## Fatos e verificação

| Fato | Fonte |
| --- | --- |
| Reports limitados a 100 requisições por minuto por conta | `docs/release-notes/2026-08-04-vtex-ads-api-reports-rate-limit.md` |
| Excedente retorna `429 Too Many Requests` | mesma nota |
| Mensagem exata: `Rate limit exceeded for this account` | mesma nota |
| Vale só para chamadas autenticadas por API Key; não afeta uso via UI | mesma nota + `docs/guides/VTEX Ads/exporting-data-from-vtex-ads/exporting-ads-reports.md` |
| Orientação: distribuir cargas históricas e syncs diários, esperar a próxima janela | mesma nota |
| Data da nota | `createdAt: 2026-08-04` |

### Antes de publicar

- ⚠️ **O documento não menciona headers de rate limit** (`X-RateLimit-Remaining`, `Retry-After`) **nem o tipo de janela** (fixa ou deslizante). O post afirma essa ausência de propósito e a transforma em argumento — mas confirme na API reference antes, porque se os headers existirem e só não estiverem na release note, o parágrafo cai.
- ⚠️ "O limite chegou depois que as integrações já existiam" é enquadramento editorial meu. A nota não diz quando o limite passou a valer, apenas que agora vale. É leitura razoável de uma release note tipo `info`, mas é leitura.
- Não há data de início de vigência além da data da nota. Não invente prazo.
