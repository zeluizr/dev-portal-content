---
titulo: "No hay cambio de schema. Igual se te rompe."
idioma: es
formato: news (tuteo)
caracteres: 1390
estado: rascunho
data_sugerida: 2026-08-26, 08:30-09:30 GMT-3
fonte_repo: docs/release-notes/2026-08-10-faststore-release-notes-4-5-0.md
---

# No hay cambio de schema. Igual se te rompe.

## Post (1390 caracteres)

"No es un cambio de schema. Ninguna query se rompe."

Eso dice el release de FastStore 4.5.0 sobre el retiro de `pagetype` en la ruta de colecciones. Es verdad. También es verdad que dos comportamientos cambian.

Uno: `StoreCollection.type` ya no devuelve `Cluster` ni `SubCategory`. Los clusters pasan a reportar `Collection`, y las categorías de tercer nivel pasan a reportar `Category`. Los dos valores del enum siguen declarados, por compatibilidad.

Dos: los slugs que agotan la cascada ahora devuelven 404. Antes, un slug de un solo segmento que no resolvía caía en búsqueda full-text.

Nada de eso rompe una query. Rompe el `if` que escribiste alrededor de la query.

Y el primer caso es el peor, justamente porque el enum sigue ahí. Un valor eliminado te da un error de compilación el día del upgrade. Un valor declarado que nunca más se emite te deja una rama muerta que nadie ejecuta y nadie nota, hasta que alguien pregunta por qué esa colección dejó de mostrar el banner.

El contrato de una API no es el schema. Es lo que tu cliente observó y asumió que iba a seguir pasando.

⚡ Dato técnico: `Cluster` y `SubCategory` siguen declarados en el enum, pero ya no se emiten. La compatibilidad es de tipo, no de comportamiento.

¿Te rompió producción alguna vez un cambio que técnicamente no era breaking?

📌 Fuente: VTEX Developer Portal — "FastStore Release Notes — Version 4.5.0"

## Hashtags

\#APIDesign #GraphQL #Arquitectura #Versionado #Backend #Ingenieria #DesarrolloWeb #Contratos #FastStore #VTEX #LATAM

## Prompt de imagem

Dark charcoal background (#1a1a1a), single coral accent. A monospace enum block listing four values — `Collection`, `Category`, `Cluster`, `SubCategory` — where the last two are dimmed to 30% opacity and marked with a small coral tag reading "declarado, nunca emitido". To the right, a thin coral arrow pointing at an unlit code branch drawn as a dead-end path. Below, small monospace caption: "el schema no cambió". Flat vector, generous negative space, no people, no logos. 1200x628.

## Agendamento

Quarta, 8h30–9h30 (GMT-3). Slot bom para o segundo maior teto. É o formato que a conta melhor converte em conversa: governança de plataforma tem as maiores taxas do ano (`dotnet-microsoft` 2,07%, `typescript` 1,32%), mesmo com alcance médio. Espere comentário, não impressão.

## Fatos e verificação

| Fato | Fonte |
| --- | --- |
| Frase citada: "Neither is a schema change (no query breaks)" | `docs/release-notes/2026-08-10-faststore-release-notes-4-5-0.md` |
| `pagetype` foi aposentado no caminho de coleção em favor da cascata tipada `by-linkid` | mesma nota |
| `StoreCollection.type` não retorna mais `Cluster` nem `SubCategory` | mesma nota |
| Clusters e coleções curadas são servidos por `collection/by-linkid`, então clusters reportam `Collection` | mesma nota |
| A resposta de categoria não expõe profundidade da árvore além da raiz, então categorias de terceiro nível reportam `Category` | mesma nota |
| Ambos os valores do enum seguem declarados, para retrocompatibilidade | mesma nota |
| Slugs que esgotam a cascata retornam `404` em vez de cair em busca full-text | mesma nota |
| Entregue na `v4.5.0` (PR #3402), dentro da feature de localização em closed beta | mesma nota |

### Antes de publicar

- ⚠️ **A mudança está dentro da seção "Localization feature (closed beta)".** O post não menciona isso e dá a entender que vale para qualquer loja na 4.5.0. Confirme o escopo antes: se o comportamento novo só se aplica a lojas com a localização ligada, o post precisa de uma linha a mais. Este é o risco factual mais sério do lote.
- ⚠️ **"Un valor eliminado te da un error de compilación" depende do cliente.** Vale para clientes com tipos gerados (codegen, TypeScript). Em cliente sem tipagem, remover o valor também passa silencioso. O argumento continua de pé, mas não é universal.
- A própria nota já orienta revisar quem faz branch em `collection { type }` ou depende do fallback de busca. O post não está denunciando algo escondido: está discutindo a definição de breaking change. Mantenha esse tom se houver contestação.
- Não afirme que a VTEX escondeu a mudança. Ela está documentada e sinalizada na release note.
