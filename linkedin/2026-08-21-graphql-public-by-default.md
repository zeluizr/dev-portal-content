---
titulo: "Público por defecto no fue un bug, fue el default"
idioma: es
formato: opinión (voseo)
caracteres: 1387
estado: rascunho
data_sugerida: 2026-08-21, 08:30-09:30 GMT-3
fonte_repo: docs/release-notes/2025-09-30-graphql-builder-update-2x.md
---

# Público por defecto no fue un bug, fue el default

## Post (1387 caracteres)

Durante años, en el builder GraphQL de VTEX IO, cada query sin anotar quedaba pública por defecto.

No fue un bug. Fue el default que alguien eligió.

En la versión 1.x, la directiva @auth era opcional. Si no la escribías, la query quedaba abierta: sin declaración de recurso, sin rol, sin nada. El silencio significaba "adelante".

En la 2.x la directiva es obligatoria y exige un argumento scope, PUBLIC o PRIVATE. Y si elegís PRIVATE, también son obligatorios productCode y resourceCode. Sin eso no compila: la CLI te frena antes del link.

Ese es el cambio real, y no es de GraphQL. Es de postura.

La industria viene migrando de "abierto salvo indicación contraria" a "cerrado salvo declaración explícita". Buckets, security groups, IAM. Siempre el mismo movimiento, siempre después del mismo incidente.

Y siempre por la misma razón: la distancia entre las dos posturas es un campo que alguien olvidó completar. Con el default permisivo, olvidarse cuesta una filtración. Con el estricto, cuesta un build roto. Prefiero el build roto.

⚡ Dato técnico: en el builder 2.x, una query sin @auth no queda pública: es un error de compilación. Y scope: PRIVATE sin productCode ni resourceCode también rompe el build.

¿Cuántos de tus endpoints son públicos porque alguien lo decidió, y cuántos porque nadie escribió nada?

📌 Fuente: VTEX Developer Portal — "GraphQL builder: update to 2.x"

## Hashtags

\#GraphQL #SecureByDefault #AppSec #Seguridad #APIDesign #Arquitectura #Backend #DesarrolloWeb #VTEX #DevSecOps #LATAM

## Prompt de imagem

Two code fragments side by side on dark charcoal background (#1a1a1a), monospace typography, single red-to-green accent shift. Left fragment, dimmed with a small grey label "1.x": a GraphQL query field with no directive, annotated below in small red text "público". Right fragment, highlighted with a green label "2.x": the same field followed by `@auth(scope: PRIVATE, productCode: "64", resourceCode: "read_account_config")`, annotated below in small green text "explícito o no compila". Flat vector, generous negative space, no people, no logos. 1200x628.

## Agendamento

Sexta, 8h30–9h30 (GMT-3). Sexta é slot fraco para alcance em público sênior, e este é o post da semana que menos depende de alcance: é isca de comentário, uma ideia só, fácil de discordar. Rende mais discussão do que impressão, e por isso aguenta o dia ruim.

## Fatos e verificação

| Fato | Fonte |
| --- | --- |
| No builder `1.x`, `@auth` é opcional e "Without the `@auth` directive, the query is public by default" | `docs/release-notes/2025-09-30-graphql-builder-update-2x.md` |
| No `2.x`, `@auth` é obrigatória e exige `scope` (`PUBLIC` ou `PRIVATE`) | mesma release note |
| `scope: PRIVATE` exige também `productCode` e `resourceCode` | mesma release note |
| CLI emite erro se faltar a diretiva, o `scope`, ou os códigos em `PRIVATE` | mesma release note |
| `graphql` builder: Stable `2.x`, Deprecated `1.x` | `.../vtex-io-documentation-builder-version-statuses.md` |
| Data anunciada da depreciação do `1.x`: 7 de janeiro de 2026 | release note de 30/09/2025 |

### Antes de publicar

- ⚠️ **Nuance importante que o post não desenvolve:** "público por padrão" no `1.x` significa sem checagem de recurso do License Manager — **não** significa que qualquer pessoa da internet chamasse qualquer query. O guia `graphql-authorization-in-io-apps.mdx` deixa claro que só apps VTEX, usuários Admin e application keys chegam a fazer requisições GraphQL autorizadas. Se alguém apontar isso nos comentários, o ponto é legítimo — responda com a distinção, não negue.
- A data 07/01/2026 vem de uma release note de setembro/2025. O post não a cita justamente porque não confirmei que foi cumprida e não adiada. Se quiser usá-la, verifique antes.
- O paralelo com buckets, security groups e IAM é meu, não do documento. É argumento, não fato citado.
