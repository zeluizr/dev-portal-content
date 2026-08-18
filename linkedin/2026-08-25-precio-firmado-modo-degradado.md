---
titulo: "Se cae el sistema de precios. ¿Qué mostrás en la vitrina?"
idioma: es
formato: opinión (voseo)
caracteres: 1398
estado: rascunho
data_sugerida: 2026-08-25, 08:30-09:30 GMT-3
fonte_repo: docs/release-notes/2026-08-10-faststore-release-notes-4-5-0.md
---

# Se cae el sistema de precios. ¿Qué mostrás en la vitrina?

## Post (1398 caracteres)

Se cae tu sistema de precios. ¿Qué mostrás en la vitrina?

Hay dos respuestas tradicionales y las dos son malas. Bajás la tienda y perdés el día. O servís el último precio que tenés en caché y rezás para que nadie compre a un valor que ya no existe.

FastStore 4.5.0 trae una tercera, y es la parte más interesante del release.

Durante un incidente del sistema de precios, Intelligent Search puede emitir un token de precio firmado. Lo nuevo es que ese token ahora viaja hasta el Checkout. El precio de la vitrina deja de ser un número suelto: llega con la prueba de que salió de un sistema legítimo, y el Checkout puede verificarla en el add-to-cart.

El cambio conceptual es chico y enorme al mismo tiempo. El dato sigue siendo viejo. Lo que deja de ser es anónimo.

Casi todos los modos degradados que vi confían en el dato por cercanía: viene de nuestro caché, entonces es nuestro. Firmarlo convierte esa confianza en algo verificable, y mueve la decisión de aceptar un precio stale al único lugar donde importa, que es donde se cobra.

El campo es opcional: si Search no lo emite, todo se comporta como antes.

⚡ Dato técnico: el token de precio firmado del Pricing Fallback ahora se propaga desde Intelligent Search hasta el Checkout.

¿Tu modo degradado sirve datos viejos, o datos viejos que se pueden verificar?

📌 Fuente: VTEX Developer Portal — "FastStore Release Notes — Version 4.5.0"

## Hashtags

\#Arquitectura #Resiliencia #SistemasDistribuidos #Backend #APIDesign #Ingenieria #Pagos #Confiabilidad #FastStore #VTEX #LATAM

## Prompt de imagem

Dark charcoal background (#1a1a1a), single violet accent. Two price tags side by side in flat vector. The left one shows a monospace number and a small grey label "caché"; the right one shows the same number plus a violet wax-seal mark and the monospace label "firmado". Between them, a thin violet line ending in an arrow labeled "checkout". Below, small monospace caption: "el dato sigue viejo, deja de ser anónimo". No people, no logos, generous negative space. 1200x628.

## Agendamento

Terça, 8h30–9h30 (GMT-3). É o post de maior teto do lote e vai no melhor slot da semana. O precedente da conta é o post de multicloud (02/12/2025): 123.957 impressões e 1,17% de engajamento, o melhor do ano — mesma veia de narrativa de falha de infraestrutura, que nunca foi aplicada a ecommerce nesta conta.

## Fatos e verificação

| Fato | Fonte |
| --- | --- |
| Intelligent Search emite um token de preço assinado durante incidente do Pricing System | `docs/release-notes/2026-08-10-faststore-release-notes-4-5-0.md` |
| FastStore agora repassa esse token até o Checkout, para o preço da prateleira ser confiável no add-to-cart | mesma nota |
| O campo é opcional; se o Search não emitir, o comportamento é igual ao das versões anteriores | mesma nota |
| Contas com a flag Pricing Fallback do Intelligent Search ligada devem garantir a flag de Pricing Fallback da loja ligada na conta | mesma nota |
| Entregue na `v4.5.0` (PR #3415) | mesma nota |

### Antes de publicar

- ⚠️ **A release note é a única fonte no repositório inteiro.** `grep -ril "pricing fallback" docs/` retorna só esse arquivo: não há guia, referência de API nem descrição do formato do token, do algoritmo de assinatura ou de quem valida. Tudo o que o post afirma sobre "verificar" é inferência a partir da palavra *signed* e de *can be trusted at add-to-cart*. Não descreva o mecanismo com mais detalhe do que isso em comentários.
- ⚠️ **"Las dos respuestas tradicionales" (bajar la tienda / servir caché) é enquadramento meu**, não está no documento.
- O post não afirma que o token impede venda a preço errado, e não deve. Diz que o Checkout pode verificar a origem. Se alguém perguntar se resolve o problema comercial de preço desatualizado, a resposta honesta é que resolve a procedência, não a atualidade.
- Pricing Fallback é feature com flag por conta. Não sugira que está ligado para todo mundo.
