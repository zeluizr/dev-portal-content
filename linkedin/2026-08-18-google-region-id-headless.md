---
titulo: "region_id de Google en storefronts headless"
idioma: es
formato: news (tuteo)
caracteres: 1387
estado: rascunho
data_sugerida: 2026-08-18, 08:30-09:30 GMT-3
fonte_repo: docs/guides/Integration-Guides/headless-commerce/adapting-headless-storefronts-to-google-raap.md
---

# region_id de Google en storefronts headless

## Post (1387 caracteres)

Si anuncias en Google Shopping con precio regional, hay una trampa en la PDP.

El cliente ve el precio de su región, hace clic y cae en una PDP con el precio nacional que le pide el código postal. Google compara aviso y landing, no coinciden, y rechaza la oferta.

Store Framework y FastStore lo resuelven solos. En headless, el trabajo es tuyo. En CMS Portal legacy, ni eso: toca migrar.

VTEX arma la URL con un parámetro region_id que es apenas un Base64 de tres partes: el prefijo fijo vtex, el país en ISO 3166-1 alpha-3 y el código postal. Decodificas dnRleDpCUkE6MDQ1NjEwMDA= y obtienes vtex:BRA:04561000.

Lo lees, guardas país y código postal en la sesión vía Session Manager y vuelves a pedir precio y stock. Nunca le pidas el código postal: ya te dijo de dónde viene al hacer clic.

Ojo: el regionId interno de VTEX y el region_id de Google no son lo mismo. El primero identifica una lista de sellers white label de una región de entrega. El segundo, solo país y código postal codificados.

⚡ Dato técnico: Base64 no es cifrado, es codificación de transporte. Cualquiera lo pega en un decoder, lee el código postal y lo edita: es sugerencia de localidad, nunca fuente de verdad de precio.

¿Tu storefront headless ya lee el region_id, o pierdes ofertas sin enterarte?

📌 Fuente: VTEX Developer Portal — "Adapting headless storefronts to Google regional price and availability"

## Hashtags

\#Ecommerce #Headless #VTEX #GoogleShopping #Frontend #JavaScript #WebPerformance #RetailTech #Arquitectura #DesarrolloWeb #LATAM

## Prompt de imagem

Minimalist technical diagram, dark charcoal background (#1a1a1a), single accent color electric blue. Left side: a browser address bar fragment showing a URL ending in `?region_id=dnRleDpCUkE6MDQ1NjEwMDA=`, the parameter highlighted. A thin arrow crosses to the right into three stacked labeled chips reading `vtex` / `BRA` / `04561000`, separated by colon glyphs. Below, small monospace caption: "Base64 ≠ cifrado". Flat vector style, generous negative space, no people, no logos, no stock-photo look. Monospace typography for all code fragments, clean sans-serif for the caption. 1200x628.

Alternativa em carrossel, 4 slides: o problema → a tabela de compatibilidade → o decode → os dois `regionId`.

## Agendamento

Terça, 8h30–9h30 (GMT-3). Cobre o começo de expediente em Santiago e Buenos Aires (25% da audiência) com Bogotá e CDMX ainda entrando. Evitar segunda (competição alta) e sexta (queda de alcance em público sênior).

## Fatos e verificação

| Fato | Fonte |
| --- | --- |
| `region_id` = `Base64(vtex:{ISO 3166-1 alpha-3}:{postalCode})` | `docs/guides/Integration-Guides/headless-commerce/adapting-headless-storefronts-to-google-raap.md` |
| `dnRleDpCUkE6MDQ1NjEwMDA=` → `vtex:BRA:04561000` | decode conferido localmente |
| Store Framework e FastStore têm suporte nativo; headless exige adaptação; CMS Portal (Legacy) não tem adaptação possível | mesmo guia, tabela de compatibilidade |
| `postalCode` e `country` já presentes na sessão pública têm precedência sobre `region_id` | mesmo guia |
| Fluxo: ler `region_id` → `POST /api/sessions` com `country` e `postalCode` → refazer busca de preço e estoque | mesmo guia |
| `regionId` interno da VTEX identifica uma lista de sellers white label de uma região de entrega (formato `v2.1DC18HE648C5111C0933734FE83EC783`) | `docs/guides/Checkout/region-section-api-quick-start-guides/get-sellers-by-region-or-address.md` |

### Antes de publicar

- Guia com `updatedAt: 2026-07-16`. Abrir a página no dev portal e confirmar que o formato do `region_id` e a precedência da sessão pública seguem iguais — o post inteiro depende disso.
- A leitura de que Base64 é público e manipulável é interpretação técnica correta, mas não está escrita nessas palavras no guia. Publicar como análise, não como citação.

## Histórico

- Tema inédito nos canais em espanhol e português (verificado em 17/08/2026).
- Adjacentes já publicados: Google UCP (12/01 e 20/04, eixo agentic commerce) e Seller White Label / Region (19/03, documento interno, não post).
