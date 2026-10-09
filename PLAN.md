# PLAN.md: passo a passo da landing da Hive

Para quem constrói (a pessoa e o agente). Regras e design: `AGENTS.md`. Textos e frases congeladas: `CONTENT.md`. Dados: `facts.json`.

**Prazos (2026-10-09 é sexta):** submissão à Colosseum em **2026-10-11**; os vídeos ainda estão por gravar (`TODO(video)`). A URL pública da landing precisa estar no ar **antes** da submissão. Planeje terminar a página, sem os vídeos, até o fim de sábado (10/10), e embutir o vídeo assim que ele existir.

## 0. O que o dono do projeto precisa entregar

O que faltar fica **oculto** na página (nunca preenchido com placeholder falso) e entra na lista final de pendências, com o marcador da equipe do MVP.

| # | Entrada | Para quê | Situação |
| --- | --- | --- | --- |
| 1 | SVGs de marca | Logotipo e símbolo | **Já estão no repositório do MVP** (`brand/logo/`, `brand/symbol/`, idênticos aos que o dono vai enviar). Usar os enviados; copiar de lá se faltar algum |
| 2 | Repositório público | Botões e links | **Pronto:** <https://github.com/Lucas-Ibanez/colosseum-hackathon-sparta> (público, Apache-2.0). `TODO(repo)` da equipe: confirmar que os jurados conseguem abrir |
| 3 | Frases congeladas F1 a F8 | Claims | **Pronto:** estão em `facts.json` → `claims`, copiadas do README do repositório |
| 4 | URLs dos vídeos (pitch, demo técnica, tomada contínua) | Seção de vídeo, botões "Watch the demo" | **Pendente** (`TODO(video)`) |
| 5 | Equipe (nome, papel, um link) e e-mail de contato | Seção "The team" | **Pendente** (`TODO(team)`); sem isso a seção fica oculta |
| 6 | Validação com usuários e modelo de negócio | Seção "Who it is for" | **Pendente** (`TODO(validation)`, `TODO(business)`). Enquanto não houver validação, a página diz "No user validation yet." O modelo de negócio não aparece |
| 7 | Revisão do português | Aprovar os textos `draft` | **Pendente** |
| 8 | Slogan em inglês | Chamada final e OG | A identidade define "Hive. Trust starts with a reason."; o repositório do MVP ainda marca `TODO(brand)`. Confirmar |
| 9 | Domínio ou hospedagem | Deploy | Recomendada |
| 10 | Logotipos de terceiros (Solana, RISC Zero, Colosseum) | Faixa "Built with" | Opcional (padrão: só texto) |

## 1. Cronograma sugerido (~13 h de trabalho)

| Quando | Etapas | Resultado |
| --- | --- | --- |
| Sexta 09/10, à noite (~5 h) | 0, 1, 2, 3 | Fundação, casca e hero funcionando em EN |
| Sábado 10/10, manhã e tarde (~6 h) | 4, 5, 6, 7, 8 | Página completa em EN e PT, sem os vídeos |
| Sábado 10/10, noite (~2 h) | 9 e embutir o vídeo | QA completo, vídeo no ar |
| Domingo 11/10, manhã (~1 h) | 10 | Deploy final, conferência dos links, URL na submissão |

**Ordem de corte** se o tempo apertar, do primeiro a cortar ao último: FAQ; ilustração de células no bloco Roadmap; diagrama de arquitetura (deixe só a lista de números); seção da equipe (só se não houver dados); animações de entrada. **Nunca cortar:** hero com a F1 e o link, os 4 passos com cartões de execução gravada, "What the program refuses", "What this doesn't show", EN e PT, links do Explorer conferidos.

## 2. Etapas

### Etapa 0. Preparação (30 a 45 min)

1. Leia `AGENTS.md`, `CONTENT.md`, `PLAN.md` e `facts.json` **inteiros**. Responda com 10 linhas do que entendeu e liste as entradas da seção 0 que ainda faltam.
2. Faça o **estudo do Bido** (`AGENTS.md`, 3.3): capturas a 1440 px e 390 px; `docs/reference-notes.md` com as observações traduzidas para os tokens da Hive e a lista do que foi descartado.
3. Confirme a stack (padrão: Astro + CSS puro).

**Pronto quando:** `docs/reference-notes.md` existe, as entradas faltantes foram listadas, nada foi codificado ainda.

### Etapa 1. Fundação (~1 h)

1. Crie o projeto e as pastas (`AGENTS.md`, 8.2). Copie `facts.json` para `src/data/`.
2. `src/styles/tokens.css` com **todos** os tokens (`AGENTS.md`, seções 4 e 5). `base.css` com reset, tipografia, foco visível, `prefers-reduced-motion`.
3. Fontes auto-hospedadas (Manrope variável e IBM Plex Mono 400, subconjunto latino), `font-display: swap`, pré-carregamento da Manrope.
4. Rotas `/` (EN) e `/pt/` (PT-BR), `src/i18n/en.json` e `pt-br.json` com as chaves de `CONTENT.md`, `scripts/check-i18n.mjs`. **As frases F1 a F8 entram no i18n por script, a partir de `facts.json`**, não por digitação.
5. SVGs em `public/brand/` e o componente `BrandMark` (um único ponto de troca).

**Pronto quando:** a página vazia abre nos dois idiomas, os tokens estão em um só arquivo, `check-i18n` falha se você apagar uma chave de propósito.

### Etapa 2. Casca (~1 h)

1. **Barra de aviso** (`announce.*`).
2. **Navegação flutuante**: logotipo horizontal, 4 âncoras, alternância **EN / PT-BR por link** (preservando a âncora), botão "Watch the demo" (ou "View the repository" enquanto não houver vídeo). Transparente sobre o hero, com fundo sólido de berinjela ao rolar. Menu para celular. Link "pular para o conteúdo".
3. **Rodapé**: colunas Produto, Projeto, Contato; licença Apache-2.0 com link; declaração de privacidade; "Hackathon prototype on Solana devnet. No real funds."

**Pronto quando:** navegação por teclado completa, alternância de idioma funciona, nenhum texto fora de `i18n`.

### Etapa 3. Hero e faixa "Built with" (~1,5 h)

1. Fundo **berinjela**, logotipo branco, eyebrow, título de 56/36 px, parágrafo de abertura (`hero.*`).
2. **F1 completa** em tamanho menor, **com o link `U6` imediatamente ao lado**, nos dois idiomas.
3. Dois botões: primário âmbar "Watch the demo" (ou "View the repository" sem vídeo); secundário "See a real settlement" (`U6`). Microtexto "Recorded runs on Solana devnet. Test USDC, no real funds."
4. **Cartão de liquidação gravada** (à direita no desktop; abaixo no celular): selo "Recorded run, 2026-10-07" e "Job P₃ `26df9ef4…`"; estado `Released`; "1 Test USDC to the executor"; "122,156 CU total, 99,541 CU in the verifier"; link "View on Explorer". Dados de `facts.json` (`U6` e `metrics`). Selo "Solana devnet".
5. Faixa **"Built with"**: texto, sem logotipos.

**Pronto quando:** em 15 segundos alguém que nunca viu o projeto entende o que a Hive faz, o link `U6` abre a transação certa na devnet, o cartão nomeia o Job e diz que é gravado, o contraste do hero passa (`AGENTS.md`, 4.2).

### Etapa 4. Problema, público e "How it works" (~2 h)

1. **"The problem"** e **"Who it is for"** (`CONTENT.md`, 4.5), curtas. Acrescente "No user validation yet…" enquanto `todo.validation` for `null`.
2. **"How it works"**: título e **quatro passos reais** numerados, cada um com título, parágrafo, linha de etiquetas em minúsculas e **cartão de execução gravada** (`CONTENT.md`, 4.6):
   - 1 Create and fund: Job P₃ `26df9ef4…`, `Funded`, 1 Test USDC, prazo de 9.000 slots, link `U3`.
   - 2 Prove locally: Job P₃, entrada `(21, 42)`, Composite 7,2 s, Groth16 177,9 s, `PASS`; rótulo "Generated locally, off-chain".
   - 3 Deliver and settle: Job P₃ `Released` (`U6`) e Job F₃ `RefundedOnFail` (`U9`).
   - 4 Timeout: Job T₃ `2c38ca66…`, `RefundedOnTimeout` (`U10`).
3. **Bloco "Roadmap (not built yet)"** logo depois dos passos, com a etiqueta (padrão do Bido, que também etiqueta o terceiro passo como roadmap). Sem cartão de dados. Ilustração opcional de duas células hexagonais, idênticas em qualquer resultado.
4. Revelação suave ao rolar (opacidade e 8 px, 300 ms), desligada com `prefers-reduced-motion`.

**Pronto quando:** cada número e link vem de `facts.json`, todo cartão diz "Recorded run" e nomeia o Job, o roadmap está marcado como não construído.

### Etapa 5. "What the program refuses", vídeo e "Verify it yourself" (~2 h)

1. **"What the program refuses"** (`#proof`): quatro cartões (`U2`, `U4`, `U5`, `U7`), cada um com o Job, o título, o nome do erro em mono, o código, quem rejeitou e o link. Legenda com a **F6** e "The Job's state was not changed."
2. **Vídeo** (`#demo`): capa e botão; `iframe` sem cookies **só após clique**. Destaque a demo técnica; ofereça pitch e tomada contínua como links secundários, se existirem. Sem URL: "Demo video coming soon" ou oculte o bloco.
3. **"Verify it yourself"** (`#verify`), três colunas:
   - Explorer: endereços do escrow, do verificador e do mint (componente de hash com cópia e valor completo) e a transação de finalização.
   - Linha de comando: bloco copiável `vericode job show --job-id <id real>` com o Job P′ de `facts.json` → `cliExamples`, e o aviso de que exige clonar e compilar a CLI.
   - Interface Hive: "Runs locally on `127.0.0.1:8710/ui/`", sem carteira no navegador.
   - A nota sobre o nome VeriCode, e links para "All cases" do README e para `docs/evidence.md`.

**Pronto quando:** os quatro links de rejeição abrem as transações certas, todo endereço é copiável, o vídeo não carrega nada de terceiros antes do clique.

### Etapa 6. "Under the hood" e limites (~1,5 h)

1. **"Under the hood"**: diagrama em SVG próprio (`CONTENT.md`, 4.10) e os números de `facts.json`.
2. **"What this shows, and what it doesn't"** (`#limits`): duas colunas. Em "shows": F2, F4, F6, F7, F8. Em "doesn't show": **F3 (obrigatória)**, F5 e a lista de limitações. **Mesmo peso visual** das demais seções.

**Pronto quando:** a F3 aparece; nenhuma frase fora das F1 a F8 afirma algo sobre o que a prova garante.

### Etapa 7. Equipe, FAQ e chamada final (~1 h)

1. **Equipe e contato**: só com dados reais; senão, oculte e liste a pendência.
2. **FAQ** (opcional): cinco perguntas de `CONTENT.md`, 4.13.
3. **Chamada final**: o slogan oficial **verbatim** em cada idioma e três botões (demo se houver, repositório, liquidação real).

**Pronto quando:** o slogan está idêntico ao de `CONTENT.md`; os botões que dependem de URL só existem se a URL existir.

### Etapa 8. Português e consistência (~1 h)

1. Revise o português contra o inglês: mesmas chaves, mesmo sentido, **sem acrescentar nem remover claims**. As frases F1 a F8 em português vêm do README em português do repositório, não de tradução sua.
2. Confirme formatos numéricos por idioma, `lang`, `hreflang`, título, descrição, Open Graph por idioma.
3. Troque de idioma em cada seção e confirme que a âncora é preservada.
4. Liste os textos `draft` para o dono aprovar.

**Pronto quando:** `check-i18n` passa e a lista de rascunhos foi entregue.

### Etapa 9. QA (~1,5 a 2 h)

1. Crie e rode `scripts/check-claims.mjs`: regex de `CONTENT.md` (seção 2), nos dois idiomas, e a conferência de que cada F1 a F8 exibida é idêntica à de `facts.json`. Revise à mão os achados da seção de limites.
2. Crie e rode `scripts/check-links.mjs`: **toda URL `explorer.solana.com` do HTML gerado precisa existir em `facts.json`** (pega erro de digitação), no formato `?cluster=devnet`.
3. **Abra manualmente** cada link de Explorer. Confirme que a transação ou conta corresponde ao rótulo e ao Job do cartão.
4. Contraste, foco, teclado, leitor de tela básico, alvos de toque.
5. Lighthouse em desktop e celular (meta ≥ 90 nas quatro categorias).
6. Larguras 390, 768, 1024 e 1440 px, sem rolagem horizontal. Teste com `prefers-reduced-motion`.
7. **Imagem OG** 1200×630 com a identidade (berinjela, logotipo horizontal branco, título). **Favicon** composto conforme `AGENTS.md`, 9.
8. Percorra a **Definição de pronto** (`AGENTS.md`, 8.5), item por item.

**Pronto quando:** os 17 itens da definição de pronto estão marcados, ou cada exceção está explicada no relatório.

### Etapa 10. Deploy e entrega (~45 min)

1. Com a autorização do dono, publique em hospedagem estática. Confira `/`, `/pt/`, os metadados sociais e o redirecionamento de `www`, se houver.
2. Embuta as URLs dos vídeos (`facts.json` → `todo`) e reconfira os blocos e botões que dependem delas.
3. Repita a conferência dos links de Explorer **no site publicado**.
4. Entregue o **relatório final**: URL pública; lista de pendências (`TODO(video)`, `TODO(team)`, `TODO(validation)`, `TODO(business)`, `TODO(brand)`, `TODO(repo)`); lista de textos `draft`; resultado do Lighthouse; qualquer desvio das regras e o motivo.

**Pronto quando:** o dono tem a URL pública para colar na submissão e o relatório final.

## 3. Mensagem inicial sugerida para o agente

> O `AGENTS.md` já foi carregado. Leia por inteiro `CONTENT.md`, `PLAN.md` e `facts.json`. Resuma em 10 linhas o que vai construir, liste as entradas da seção 0 do plano que ainda faltam e execute apenas as Etapas 0 e 1. Ao fim de cada etapa, mostre o checklist "Pronto quando", aponte qualquer desvio e **pare** para eu aprovar a próxima.

## 4. Riscos conhecidos

| Risco | Mitigação |
| --- | --- |
| Os vídeos só ficam prontos em 10/10 | Bloco de vídeo pronto, com "coming soon" e botões alternativos até a URL existir; embutir na Etapa 10 |
| O README do MVP mudar antes da submissão | `facts.json` e `CONTENT.md` são derivados dele; se mudar, regenerar. O README sempre vence |
| Slogan em inglês ainda `TODO(brand)` no repositório do MVP | Usar o da identidade e listar a confirmação como pendência |
| SVGs provisórios | Um único componente `BrandMark`; troca por arquivo do mestre sem mexer em seções |
| A página parecer "clone" do Bido | Só a estrutura vem do Bido; cores, tipografia, formas, textos, logotipo e dados são da Hive |
| Tentação de exagerar claims | Frases F1 a F8 importadas, `check-claims`, regra do link `U6` junto à F1 |
| Dados gravados lidos como ao vivo | Todo cartão diz "Recorded run", data e Job |
| `AGENTS.md` truncado pelo Codex (limite de 32 KiB) | Manter abaixo de 28 KB; o restante vive em `CONTENT.md`, `PLAN.md` e `facts.json` |
