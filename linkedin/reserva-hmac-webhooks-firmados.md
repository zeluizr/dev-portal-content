---
titulo: "Firmás tus webhooks, pero validás la firma tarde"
idioma: es
formato: opinión (voseo)
caracteres: 1397
estado: reserva
data_sugerida: semana de 2026-08-24, terça 08:30-09:30 GMT-3
fonte_repo: docs/guides/b2b/b2b-buyer-portal/b2b-password-migration.md
---

# Firmás tus webhooks, pero validás la firma tarde

## Post (1397 caracteres)

Firmás tus webhooks con HMAC. Pero validás la firma después de consultar la base de datos.

Felicitaciones: construiste un oráculo.

Encontré en la documentación de VTEX un protocolo que funciona como el checklist de todo lo que se hace mal con webhooks firmados.

La firma se calcula sobre una canonical string de seis líneas: método, path, client id, timestamp, nonce y el SHA-256 del body. Y el hash va sobre los bytes crudos del body. Textual: no parsees ni vuelvas a serializar el JSON. Re-serializar cambia el hash y te rompe la verificación sin que entiendas por qué.

El timestamp se valida en una ventana de ±300 segundos, y el nonce no puede haber aparecido antes para ese client id dentro de esa ventana. Eso es lo que corta el replay, no la firma sola.

La comparación es en tiempo constante. Y la verificación va antes de cualquier consulta al sistema legado, no después.

El contrato se reduce a tres códigos. "El usuario no existe" y "la contraseña está mal" devuelven el mismo 401, indistinguibles. Sin eso, tu endpoint es un enumerador de usuarios gratis.

⚡ Dato técnico: el presupuesto total de respuesta es 3 segundos duros, con objetivos p95 ≤ 1s y p99 ≤ 2,5s. Verificar el HMAC cuesta menos de 10ms. No hay excusa de performance para dejarlo al final.

¿Tu servicio valida la firma antes o después de tocar la base?

📌 Fuente: VTEX Developer Portal — "B2B password migration"

## Hashtags

\#Seguridad #Webhooks #HMAC #AppSec #APIDesign #Autenticacion #Backend #Arquitectura #DevSecOps #VTEX #LATAM

## Prompt de imagem

Vertical flow diagram on dark charcoal background (#1a1a1a), single lime accent. Two parallel paths from a single inbound request node. Left path, dimmed grey and marked with a small red cross: request → "consulta a la base" → "verifica firma". Right path, lime and marked with a check: request → "verifica firma (<10ms)" → "consulta a la base". Below, a thin monospace strip listing the canonical string lines: `METHOD / PATH / CLIENT-ID / TIMESTAMP / NONCE / SHA256(body)`. Flat vector, generous negative space, no people, no logos. 1200x628.

## Agendamento

Reserva — não entra nesta semana. Vale um slot nobre (terça ou quarta) da semana seguinte, e não a sexta desta, porque é o post com o conteúdo técnico mais denso do lote e merece dia de alcance cheio.

## Fatos e verificação

| Fato | Fonte |
| --- | --- |
| HMAC-SHA256, assinatura em Base64 | `docs/guides/b2b/b2b-buyer-portal/b2b-password-migration.md` |
| Canonical string de 6 linhas: método, path, `X-VTEX-Client-Id`, `X-VTEX-Timestamp`, `X-VTEX-Nonce`, SHA-256 do body | mesma seção |
| Hash sobre os bytes crus: "Don't parse or re-serialize the JSON" | mesma seção |
| Validar timestamp em ±300s (recomendado) | "Middleware verification steps" |
| Nonce não pode ter sido visto antes para aquele `ClientId` na janela | mesma lista |
| Comparação em tempo constante | mesma lista |
| HMAC antes de qualquer consulta ao legado | seção "Latency and timeouts" |
| 3 segundos hard requirement; p95 ≤ 1s; p99 ≤ 2,5s; HMAC < 10ms | mesma seção |
| Só `200`, `401`, `403`; "user not found" e "wrong password" ambos `401`, indistinguíveis, para impedir enumeração | seção "Response contract" |
| TLS 1.3 obrigatório; segredo de 32+ bytes; proibido logar segredo, senha ou assinatura | seção "Security requirements" |

### Antes de publicar

- ⚠️ **O documento tem callout de disponibilidade restrita** ("available only for stores using B2B Buyer Portal, currently available for selected accounts"). Não apresente como comportamento geral da plataforma. O post já evita isso ao tratar o doc como estudo de caso, não como anúncio — mantenha o enquadramento.
- O `< 10ms` do custo do HMAC é estimativa do próprio documento ("typically < 10ms"), não medição publicada.
- Houve commit em 05/08/2026 corrigindo links dos endpoints da Authenticator API nesse guia. Confirme que o cálculo de assinatura publicado na API reference bate com o do guia antes de postar.
- O doc é de 16/06/2026 — fora da janela de 45 dias. Entrou pelo peso atemporal dos números, não por ser notícia. Não escreva "esta semana" nem "acaban de publicar".
