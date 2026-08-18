---
titulo: "Tu build pasó. Tu fuente no llegó."
idioma: es
formato: news (tuteo)
caracteres: 1230
estado: rascunho
data_sugerida: 2026-08-24, 12:00-13:00 GMT-3
fonte_repo: docs/release-notes/2026-08-10-faststore-release-notes-4-5-0.md
---

# Tu build pasó. Tu fuente no llegó.

## Post (1230 caracteres)

Tu build pasó. Tu deploy pasó. Tu fuente no llegó.

Durante varias versiones, el `copyPublicFiles` del CLI de FastStore descartaba directorios anidados y extensiones que no coincidían. El resultado: las fuentes self-hosted que vivían en `public/fonts/` nunca llegaban al build de producción.

Ningún error. Ningún warning. El pipeline en verde.

Lo que fallaba después era el navegador, cayendo al fallback de la familia tipográfica. Un bug que no aparece en los logs, aparece en la pantalla. Y normalmente lo reporta alguien de marca, no alguien de ingeniería.

Eso es lo incómodo de las fallas silenciosas de build: tu CI verifica que el proceso terminó con código 0, no que el artefacto salió completo. Son dos preguntas distintas y casi nadie hace la segunda.

La 4.5.0 lo corrige: copia directorios anidados y los formatos .woff, .woff2, .ttf, .otf y .eot. Si tienes fuentes o assets anidados en `public/`, actualiza y vuelve a correr el build.

⚡ Dato técnico: `copyPublicFiles` descartaba subdirectorios de `public/`. Un `public/fonts/inter.woff2` no llegaba al bundle de producción.

¿Qué verifica tu pipeline, además de que el comando no falló?

📌 Fuente: VTEX Developer Portal — "FastStore Release Notes — Version 4.5.0"

## Hashtags

\#Frontend #WebPerformance #BuildTools #CI #DesarrolloWeb #DevOps #Tipografia #FastStore #VTEX #LATAM

## Prompt de imagem

Dark charcoal background (#1a1a1a), single dusty rose accent. A simple file-tree diagram in monospace on the left: `public/` with a nested child `fonts/inter.woff2`, the nested line struck through in dusty rose. An arrow labeled `build` points right to a second tree containing only the top-level file. Below, a small monospace caption: "exit code 0". Flat vector, generous negative space, no people, no logos. 1200x628.

## Agendamento

Segunda, meio-dia (GMT-3). É o post de menor teto do lote e vai no pior slot de propósito. O histórico de 12 meses da conta é explícito sobre isso: os quatro posts de ferramental (`githubactions-devops-ci` 0,12%, `opensource-vibecoding` 0,14%, `git-github-javascript` 0,17%, `tecnología-github-desarrolloweb` 0,17%) estão entre os oito piores em taxa de engajamento do ano. Não se espera alcance daqui. Serve de aquecimento e é o primeiro a cortar se a semana apertar.

## Fatos e verificação

| Fato | Fonte |
| --- | --- |
| `@faststore/cli` `copyPublicFiles` descartava diretórios aninhados e extensões que não batiam | `docs/release-notes/2026-08-10-faststore-release-notes-4-5-0.md` |
| Fontes self-hosted em `public/fonts/` nunca chegavam ao build de produção | mesma nota |
| Formatos agora copiados: `.woff`, `.woff2`, `.ttf`, `.otf`, `.eot` | mesma nota |
| Diretórios aninhados agora copiados corretamente | mesma nota |
| Correção entregue na `v4.5.0` (PR #3412); lojas devem atualizar e refazer o build | mesma nota |

### Antes de publicar

- ⚠️ **"Ningún error. Ningún warning. El pipeline en verde." é dedução minha.** A nota diz que os arquivos eram descartados, não diz que o processo terminava sem aviso. É a leitura mais provável de um bug de cópia silenciosa, mas não está escrito. Se quiser blindar, troque por "el proceso terminaba igual".
- ⚠️ **O fallback tipográfico no navegador também é dedução.** É a consequência óbvia de uma fonte ausente, mas o documento não descreve o sintoma no cliente.
- O exemplo `public/fonts/inter.woff2` é ilustrativo. A nota cita `public/fonts/` como caminho, não um arquivo específico.
- A nota não diz desde qual versão o bug existia. O post usa "durante varias versiones" — se for questionado, não tenho número. Considere remover.
