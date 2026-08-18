# LinkedIn — pauta semanal

Rascunhos em espanhol para audiência sênior de LatAm, garimpados do repo de conteúdo da VTEX.
Regra de ouro: a VTEX é **fonte de dado técnico**, nunca protagonista. Se a pauta só faz sentido
para quem já opera VTEX, ela não entra.

## Semana de 24 a 28 de agosto de 2026

| Dia | Post | Formato | Chars | Teto | Arquivo |
| --- | --- | --- | --- | --- | --- |
| Seg 24, 12h | Tu build pasó. Tu fuente no llegó. | news (tuteo) | 1230 | 3 | [`2026-08-24-faststore-fuentes-nunca-llegaron-al-build.md`](2026-08-24-faststore-fuentes-nunca-llegaron-al-build.md) |
| Ter 25, 8h30 | Se cae el sistema de precios. ¿Qué mostrás en la vitrina? | opinión (voseo) | 1398 | 9 | [`2026-08-25-precio-firmado-modo-degradado.md`](2026-08-25-precio-firmado-modo-degradado.md) |
| Qua 26, 8h30 | No hay cambio de schema. Igual se te rompe. | news (tuteo) | 1390 | 8 | [`2026-08-26-no-hay-cambio-de-schema.md`](2026-08-26-no-hay-cambio-de-schema.md) |
| Qui 27, 8h30 | Webhooks firmados (reserva da semana anterior) | opinión (voseo) | 1397 | 7 | [`reserva-hmac-webhooks-firmados.md`](reserva-hmac-webhooks-firmados.md) |
| Sex 28, 8h30 | Una feature, dos maneras de ensayarla | news (tuteo) | 1383 | 6 | [`2026-08-28-dpready-dplive-dos-ensayos.md`](2026-08-28-dpready-dplive-dos-ensayos.md) |

**Descartado:** [`descartado-vtex-tracking-docs-eliminados.md`](descartado-vtex-tracking-docs-eliminados.md) —
a premissa não sobreviveu à verificação. O arquivo fica como registro para não regarimpar a mesma
pauta daqui a um mês.

### Origem do lote

Quatro das cinco pautas saíram de um único arquivo: `docs/release-notes/2026-08-10-faststore-release-notes-4-5-0.md`
(três) e a guia de Delivery Promise reescrita em 14/08 (uma). O `main` do upstream não recebe commit
desde 14/08, então esta semana **não depende de nenhum merge novo**.

### Lógica do calendário

Mesma regra da semana anterior: os dois slots ruins (segunda e sexta) levam os dois menores tetos,
terça/quarta/quinta levam os três maiores. A novidade é que o teto agora tem lastro no relatório de
desempenho da conta, não só em julgamento editorial — ver abaixo.

Alternância de formato: news → opinión → news → opinión → news. Eixos: build → resiliência/preço →
contrato de API → segurança → rollout. Nenhum eixo se repete em dias seguidos e nenhum deles foi
usado na semana de 17 a 21.

## Baseline de desempenho (relatório de 19/08/2025 a 18/08/2026)

1.178.297 impressões, 415.013 pessoas alcançadas, 2.874 seguidores. O relatório lista **50
publicações** e o piso é 4.766 impressões — qualquer post abaixo disso não aparece, então isto **não
é o histórico completo**. As hashtags vêm da URL (só as três primeiras), não do texto.

O que o dado mudou nas decisões:

- **Ferramental de build/CI é o pior cluster do ano.** `githubactions-devops-ci` 0,12%,
  `opensource-vibecoding` 0,14%, `git-github-javascript` 0,17%, `tecnología-github-desarrolloweb`
  0,17% — quatro dos oito piores em taxa de engajamento. Por isso o post de fontes caiu de teto 6
  para 3 e foi para segunda.
- **Narrativa de falha de infraestrutura é a melhor veia.** `multicloud-aws-googlecloud`: 123.957
  impressões e 1,17%, o melhor post do ano por larga margem. O post de terça é a primeira aplicação
  dessa veia a ecommerce.
- **Governança de plataforma converte em comentário, não em alcance.** `dotnet-microsoft` 2,07% (a
  maior taxa do ano) e `typescript` 1,32%, ambos com alcance médio. É o perfil do post de quarta.
- **`#ecommerce` não é motor de alcance.** Os dois posts de desenvolvimento web marcados com ela
  ficaram em 0,40% e 0,16%, contra 0,66% do equivalente sem a tag. Enquadrar como
  arquitetura/resiliência tem histórico melhor — o que reforça a regra de ouro por outro caminho.
- **Contexto de retomada.** O último post do relatório é de 06/07/2026 e as impressões diárias caíram
  de 4.000–8.000 no início de julho para 200–400 desde meados do mês. A conta está em vale de
  alcance; não compare os números destas semanas com os picos de dezembro a março.

## Semana de 17 a 21 de agosto de 2026

| Dia | Post | Formato | Chars | Teto | Arquivo |
| --- | --- | --- | --- | --- | --- |
| Seg 17, 12h | 100 requests por minuto, anunciados después | news (tuteo) | 1289 | 6 | [`2026-08-17-vtex-ads-rate-limit.md`](2026-08-17-vtex-ads-rate-limit.md) |
| Ter 18, 8h30 | region_id de Google en storefronts headless | news (tuteo) | 1387 | 8 | [`2026-08-18-google-region-id-headless.md`](2026-08-18-google-region-id-headless.md) |
| Qua 19, 8h30 | Cuatro años congelado en TypeScript 3.9.7 | opinión (voseo) | 1394 | 8 | [`2026-08-19-node-builder-typescript-congelado.md`](2026-08-19-node-builder-typescript-congelado.md) |
| Qui 20, 8h30 | Sacaron una cookie y la latencia bajó 60% | news (tuteo) | 1399 | 8 | [`2026-08-20-intelligent-search-cookie-cdn.md`](2026-08-20-intelligent-search-cookie-cdn.md) |
| Sex 21, 8h30 | Público por defecto no fue un bug | opinión (voseo) | 1387 | 7 | [`2026-08-21-graphql-public-by-default.md`](2026-08-21-graphql-public-by-default.md) |

⚠️ **Ajuste pendente no post de quarta 19.** O único precedente de TypeScript na conta
(`typescript-javascript-desarrolloweb`, 31/10/2025) teve boa taxa (1,32%) e alcance baixo (5.894
impressões). Não é repetição — ângulo diferente, 10 meses de distância — mas se as hashtags forem
`#typescript #javascript #desarrolloweb`, o alcance provavelmente repete. O eixo de deprecação e
runtime legado conversa melhor com `dotnet-microsoft` (20,5k, 2,07%) e `linux-opensource` (15k, 1,02%).

### Lógica do calendário

Os dois slots ruins recebem os dois posts de menor teto. Segunda tem competição alta e sexta cai
em alcance com público sênior, então segunda leva o rate limit (formato curto, dado seco) e sexta
leva o GraphQL (uma ideia só, isca de comentário — rende discussão mesmo em dia fraco).
Terça, quarta e quinta ficam com os três de teto 8.

O horário 8h30–9h30 GMT-3 cobre início de expediente em Santiago e Buenos Aires (25% da audiência)
com Bogotá e CDMX ainda entrando.

## Estrutura de cada arquivo

- **Post** — texto pronto para copiar, 900–1400 caracteres **incluindo** a linha `📌 Fuente`
- **Hashtags** — bloco separado
- **Prompt de imagem** — 1200x628, estilo consistente (fundo carvão `#1a1a1a`, um acento por post;
  já usados: laranja, azul elétrico, teal, âmbar, lima, vermelho→verde, rosa, violeta, coral, ciano)
- **Agendamento** — dia, horário e por quê
- **Fatos e verificação** — cada afirmação do post mapeada para o arquivo de origem no repo
- **Antes de publicar** — o que checar em fonte primária, e o que no post é análise minha e não citação

## Avisos que valem para o lote todo

- ⚠️ **Nenhum post foi verificado contra o dev portal publicado.** Todos saíram de `git show main:` do
  repo de conteúdo. Antes de publicar cada um, confira a seção "Antes de publicar" do arquivo.
- ⚠️ **O risco factual mais sério do lote de 24 a 28 está no post de quarta:** a mudança de
  `pagetype` está documentada dentro da seção "Localization feature (closed beta)" e o post não diz
  isso. Confirme o escopo antes de publicar.
- ⚠️ **Vários posts contêm enquadramento editorial que não está escrito nos documentos.** Estão
  sinalizados individualmente em cada arquivo. São defensáveis, mas são leitura, não citação.
- Esta pasta está dentro de um fork que sincroniza com o `upstream` da VTEX. Se commitar no `main`,
  isso viaja em todo rebase e pode acabar num PR por acidente. Considere `linkedin/` no `.gitignore`
  ou uma branch separada.
