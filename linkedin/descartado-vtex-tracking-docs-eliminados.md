---
titulo: "Documentación eliminada como señal de producto"
idioma: es
formato: opinión (voseo)
caracteres: 0
estado: descartado
data_sugerida: —
fonte_repo: commit 2b7d580fa (Delete docs/guides/Fulfillment/vtex-tracking directory)
---

# Documentación eliminada como señal de producto — DESCARTADA

## Por que não vira post

A pauta era: em 11/08/2026 o diretório `docs/guides/Fulfillment/vtex-tracking/` inteiro foi apagado
(2 arquivos, 77 linhas), e documentação removida costuma anteceder produto descontinuado. O ângulo
seria "leia o repositório de docs do seu fornecedor como leading indicator do roadmap".

**A verificação derrubou a premissa.** O produto continua documentado:

```
$ grep -ril "vtex tracking" docs/
docs/guides/VTEX-Tracking/vtex-tracking-overview.md      ← existe, e é anterior à remoção
docs/release-notes/vtex-tracking-api-changes-in-all-paths.md
docs/guides/Fulfillment/vtex-shipping-network/tracking-1.md
docs/guides/Fulfillment/vtex-shipping-network/integration-flow.md
```

O arquivo apagado (`vtex-tracking.md`) tinha 10 linhas e era só um ponteiro para o help center, com
`createdAt` de 2021. O outro (`integrate-external-orders-vtex-tracking.md`) apontava para um guia
que vive na API reference. Ou seja: a remoção é consolidação de duplicata, exatamente o mesmo
movimento dos commits `7eacc8e76` ("remove duplicate configure-tradename article") e `13841492b`
("Remove CMS local setup and development document") das mesmas duas semanas.

Publicar "apagaram os docs, o produto vai morrer" seria errado nos fatos e visível para qualquer
pessoa da VTEX na audiência — e a VTEX é a empresa mais representada entre os seguidores da conta
(2%, topo do relatório de dados demográficos). Custo de reputação alto, teto de alcance baixo.

## O que reviveria a pauta

- Se `docs/guides/VTEX-Tracking/vtex-tracking-overview.md` também for removido, ou marcado
  `hidden: true`, sem destino equivalente.
- Se aparecer release note de depreciação ou anúncio no help center.
- Se a API reference de tracking sair do portal.

Até lá, o padrão que o repositório mostra é limpeza de duplicata, não descontinuação. Vale
reexaminar em um mês.

## Nota de método

Esta pauta entrou na lista com risco sinalizado desde o começo e saiu na primeira verificação.
Um `grep -ril` de dez segundos foi o que separou uma tese elegante de uma afirmação falsa —
o passo de checagem contra a fonte primária não é formalidade.
