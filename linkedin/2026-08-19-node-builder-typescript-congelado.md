---
titulo: "Cuatro años congelado en TypeScript 3.9.7"
idioma: es
formato: opinión (voseo)
caracteres: 1394
estado: rascunho
data_sugerida: 2026-08-19, 08:30-09:30 GMT-3
fonte_repo: docs/guides/vtex-io/Reference/concepts/vtex-io-documentation-builders/
---

# Cuatro años congelado en TypeScript 3.9.7

## Post (1394 caracteres)

Durante cuatro años, las apps backend de VTEX IO compilaron con TypeScript 3.9.7.

Esa versión salió en mayo de 2020. Los builders 3.x, 4.x y 6.x compartían el mismo compilador congelado, sin importar que el runtime debajo fuera Node 8, Node 12 o Node 16. El motor cambiaba. El lenguaje que te dejaban escribir, no.

VTEX ya marcó el builder 6.x como deprecated. El 7.x, estable, corre Node 20 y TypeScript 5.5.3.

Y no es el caso raro de una plataforma puntual. Es lo que pasa cuando adoptás una plataforma gestionada: no elegís solo dónde corre tu código, elegís qué versión del lenguaje tenés permitido escribir. El intervalo entre el fin de soporte upstream y el fin de soporte de la plataforma es deuda técnica que no contrajiste vos.

Y ojo con lo que significa deprecated: las apps existentes siguen corriendo y podés publicar minors y patches, pero no crear apps nuevas ni majors nuevos. Es una puerta que se cierra despacio, y por eso nadie la mira hasta que la necesita abierta.

⚡ Dato técnico: pasar del builder 6.x al 7.x mueve la app de TypeScript 3.9.7 (mayo 2020) a 5.5.3 (julio 2024), y de Node 16 a Node 20. Los errores de tipado que vas a comer no son bugs nuevos: son cuatro años de chequeos que nunca corriste.

¿Cuánto tiempo pasa entre que una versión muere upstream y muere en tu plataforma?

📌 Fuente: VTEX Developer Portal — "Builder version statuses" y "Node builder"

## Hashtags

\#TypeScript #NodeJS #JavaScript #BackendDevelopment #DeudaTecnica #PlatformEngineering #Arquitectura #DesarrolloWeb #VTEX #DevOps #LATAM

## Prompt de imagem

Minimalist technical timeline on dark charcoal background (#1a1a1a), single amber accent. A horizontal line with four milestone markers labeled in monospace: "TS 3.9.7 — may 2020", "TS 4.x", "TS 5.0", "TS 5.5.3 — jul 2024". The first three quarters of the line are rendered as a flat dim grey bar labeled "builder 3.x / 4.x / 6.x", the final segment in amber labeled "builder 7.x". Below, small caption in monospace: "el runtime cambió tres veces. el compilador, ninguna." Flat vector, generous negative space, no people, no logos. 1200x628.

## Agendamento

Quarta, 8h30–9h30 (GMT-3). É o slot mais forte da semana e este é o post de maior teto — encosta no tema de 43.449 impressões (JavaScript / desarrollo web) e carrega o elemento de conflito plataforma vs. autonomia do time.

## Fatos e verificação

| Fato | Fonte |
| --- | --- |
| Builders `3.x`, `4.x` e `6.x` usam TypeScript `3.9.7` | `.../vtex-io-documentation-node-builder.md`, tabela de versionamento |
| Builder `6.x` = Node.js 16 + `@types/node` 12.0.0 | mesma tabela |
| Builder `7.x` = Node.js 20 + `@types/node` 20.0.0 + TypeScript `5.5.3` | mesma tabela |
| `3.x` e `4.x` = Decommissioned; `6.x` = Deprecated; `7.x` = Stable | `.../vtex-io-documentation-builder-version-statuses.md` |
| Deprecated = roda e aceita minor/patch, mas bloqueia app novo ou major novo | mesma tabela de status |
| TypeScript 3.9 lançado em maio/2020; 5.5 em julho/2024 | conhecimento externo, não está no repo |

### Antes de publicar

- ⚠️ **Não afirme uma data para a deprecação do 6.x.** O commit que mudou o status é de 13/08/2026, mas o release note original de 10/10/2024 já anunciava "Node builder 6.x deprecation date: June 2025", e o frontmatter do arquivo de status marca `updatedAt: 2026-03-09`. As três datas não fecham. O post evita a questão de propósito — mantenha assim.
- ⚠️ **Contradição dentro do repo:** a tabela em `vtex-io-documentation-node-builder.md` ainda lista o `6.x` com status `Stable until June 2025`, enquanto o arquivo de status diz `Deprecated`. Confirme no dev portal qual está vigente.
- "Node 16 ya no recibe soporte de la comunidad" é verdade e está redigido sem data justamente porque a data **não está no repo**. Se quiser citar setembro/2023, confirme na nodejs.org antes.
- "Miles de apps" é estimativa retórica. Não há número de apps no repo. Se incomodar, troque por "las apps backend de VTEX IO".
