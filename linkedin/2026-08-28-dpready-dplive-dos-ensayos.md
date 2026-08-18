---
titulo: "Una feature, dos maneras de ensayarla"
idioma: es
formato: news (tuteo)
caracteres: 1383
estado: rascunho
data_sugerida: 2026-08-28, 08:30-09:30 GMT-3
fonte_repo: docs/guides/Search/setting-up-delivery-promise-components.md
---

# Una feature, dos maneras de ensayarla

## Post (1383 caracteres)

Una feature nueva de búsqueda, y dos maneras distintas de ensayarla antes de que toque tráfico real.

VTEX reescribió esta semana la guía de activación de Delivery Promise, y lo que me llamó la atención no es la feature. Es el mecanismo.

La cuenta entra primero en `DpReady`. La funcionalidad existe y se puede probar, pero las requests de búsqueda en producción no cambian. Recién después de validar, la cuenta pasa a `DpLive`.

Lo interesante es que el ensayo cambia según el stack. Con el framework, validas en un workspace de desarrollo mientras `master` sigue sirviendo tráfico sin Delivery Promise. En headless no hay workspace, así que el ensayo es un parámetro: `dpPreview=true` en la request de Intelligent Search. Y mientras previsualizas, la respuesta te devuelve `deliveryPromiseEnabled: false`.

Es la misma idea implementada dos veces. Aislamiento por entorno de un lado, aislamiento por request del otro. Cuando no puedes separar los ambientes, separas las llamadas.

Un detalle que sí discuto: los dos estados los aplica Soporte, por ticket. El ensayo es autoservicio. El interruptor no.

⚡ Dato técnico: en headless, `dpPreview=true` solo existe en Intelligent Search API v1. No está en la Legacy.

¿Tus flags de rollout son autoservicio, o dependen de que alguien del proveedor los mueva?

📌 Fuente: VTEX Developer Portal — "Setting up Delivery Promise components"

## Hashtags

\#FeatureFlags #Rollout #DarkLaunch #Arquitectura #Backend #APIDesign #Ingenieria #Headless #VTEX #LATAM

## Prompt de imagem

Dark charcoal background (#1a1a1a), single cyan accent. Two horizontal lanes in flat vector. The top lane shows a box labeled `master` carrying a steady stream of dots, with a separate branch box labeled `workspace` receiving a single cyan dot. The bottom lane shows one request arrow with a cyan query-string tag reading `dpPreview=true` splitting off from the same stream. A vertical divider between the lanes carries the monospace labels `DpReady` above and `DpLive` below. Generous negative space, no people, no logos. 1200x628.

## Agendamento

Sexta, 8h30–9h30 (GMT-3). Sexta cai em alcance com público sênior, e este é o segundo menor teto do lote — os dois slots ruins levam os dois menores, como na semana passada. A pergunta final é isca de comentário deliberada: quase todo mundo tem uma história de flag que dependia de ticket.

## Fatos e verificação

| Fato | Fonte |
| --- | --- |
| `DpReady` é o estado inicial que o Suporte aplica na conta; a feature fica disponível para teste e as requests de busca em produção não são afetadas | `docs/guides/Search/setting-up-delivery-promise-components.md` |
| `DpLive` é o estado de produção; exige contatar o Suporte de novo para promover de `DpReady` | mesma guia |
| Validação em workspace de desenvolvimento enquanto `master` segue servindo produção | mesma guia |
| Em produção, respostas de busca retornam `deliveryPromiseEnabled: true` | mesma guia |
| Headless usa `dpPreview=true` na query; durante o preview a resposta retorna `deliveryPromiseEnabled: false` | `docs/guides/Search/delivery-promise-for-headless-stores.md` |
| `dpPreview` só é suportado na Intelligent Search API v1, não na Legacy | mesma guia headless |
| Guia de setup reescrita em 14/08/2026 (`updatedAt`) | frontmatter do arquivo |
| Delivery Promise está em open beta | guia headless |

### Antes de publicar

- ⚠️ **O post não menciona que Delivery Promise está em open beta**, e a guia headless ainda avisa que os filtros de sidebar podem sofrer breaking changes. Se o assunto for tratado como recurso estável nos comentários, corrija.
- ⚠️ **"Los dos estados los aplica Soporte, por ticket" é literal na documentação, mas a crítica implícita é minha.** Ativação por ticket em feature de open beta é prática comum e defensável. Não transforme em denúncia: o ponto é sobre quem controla o interruptor, não sobre má-fé.
- ⚠️ **Não confundi os dois mecanismos de propósito, mas eles vêm de arquivos diferentes.** `DpReady`/`DpLive` estão na guia de componentes (Store Framework); `dpPreview` está na guia headless. O paralelo entre os dois é leitura minha — nenhum dos dois documentos apresenta os mecanismos como duas faces da mesma decisão.
- A guia de setup não diz que `dpPreview` funciona em loja com framework, e a guia headless não menciona `DpReady`. Não afirme que dá para combinar os dois.
