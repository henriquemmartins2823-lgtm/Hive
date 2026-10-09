# AGENTS.md: landing page da Hive

Instruções para o agente de código que constrói a landing page da Hive. Leia este arquivo **inteiro** antes de escrever qualquer linha.

## 0. Leitura obrigatória e ordem de verdade

O Codex carrega este arquivo sozinho (e só ele, até 32 KiB). Os demais você **abre e lê por inteiro** antes de começar e antes de cada etapa do `PLAN.md`:

1. `AGENTS.md` (este arquivo): regras, design, stack e critérios de pronto.
2. `CONTENT.md`: textos em inglês e português, as frases congeladas F1 a F8 e as frases proibidas.
3. `facts.json`: **única fonte** de números, endereços, links de transação e das frases F1 a F8.
4. `PLAN.md`: o passo a passo, com prazos e critérios de "pronto quando".

**Fonte da verdade do produto:** o repositório do MVP, <https://github.com/Lucas-Ibanez/colosseum-hackathon-sparta> (público, Apache-2.0). Se `CONTENT.md` ou `facts.json` divergirem do `README.md` desse repositório (seção "Frozen phrases") ou de `docs/README.pt-BR.md`, **o README vence**: pare e avise o dono. Não altere o repositório do MVP; ele é só leitura para você.

Se dois arquivos se contradisserem: `CONTENT.md` e `facts.json` vencem sobre fatos e claims; este arquivo vence sobre design e processo. Se a contradição não se resolver assim, **pare e pergunte** ao dono do projeto. Não escolha por conta própria.

## 1. Missão

Construir a landing da **Hive** para a submissão ao **Hackathon da Colosseum** (prazo: **2026-10-11**; vídeo definitivo previsto para 2026-10-10). Todo o material da submissão é em **inglês**; o site existe também em **português do Brasil**.

A Hive é um **escrow em Solana devnet**: o comprador deposita Test USDC, o executor entrega um artefato e uma prova RISC Zero do resultado, e o programa só libera o dinheiro depois de conferir o vínculo e **verificar a prova Groth16 por CPI**, na mesma transação.

**O que a página precisa conseguir, nesta ordem:**

1. Em ~15 segundos, um jurado técnico entende **o que a Hive faz** e vê que é **real** (transações no Explorer, números medidos).
2. Em ~2 minutos, ele consegue **conferir** o que foi dito (links, endereços, comandos) e vê **os limites** declarados.
3. Ele sai com o vídeo, o repositório e o Explorer a um clique.

Público principal: jurados do hackathon (técnicos, conhecem Solana). Público secundário: o ICP declarado pela equipe, tech leads e sócios de software houses nativas de IA que delegam tarefas a agentes, e operadores de plataformas de jobs. **Esta não é uma página de vendas**: não há clientes, pilotos, preços nem depoimentos, e ainda **não há validação com usuários**.

## 2. Regras invioláveis (verdade e honestidade)

A marca se baseia em "Confiança começa com um porquê". Uma landing que exagera destrói isso. Estas regras valem acima de qualquer preferência de design.

### 2.1 Claims

- As únicas afirmações sobre o que a Hive faz e prova são as **frases F1 a F8**, ratificadas pela equipe do MVP e copiadas em `facts.json` → `claims.phrases` (EN e PT). **Importe-as de lá; nunca as redigite.** Não crie, não reforce, não suavize, não reescreva. Paráfrase só se **não disser mais** do que a frase.
- **Sempre que a F1 (ou a expressão "verified on-chain") aparecer, o link de uma transação real (`facts.json` → `U6`) deve estar imediatamente ao lado.** A F6 sempre vem com os links das quatro rejeições.
- **Todo dado de transação é de uma execução gravada**, não ao vivo. Rotule cada cartão "Recorded run" / "Execução gravada" com a data (2026-10-07) e **nomeie o Job** (por exemplo, Job P₃ `26df9ef4…`). Nunca mostre receipt, estado ou transação sem dizer de qual Job é.
- Tudo que envolve dinheiro diz **Test USDC** e **devnet** no mesmo bloco de texto. Nunca "USDC" sozinho.
- O que ainda não existe aparece sob a etiqueta **Roadmap (not built yet)** / **Roadmap (ainda não construído)**, dito como futuro ("next", "we plan to"). Nada de roadmap sem etiqueta.
- **Frases proibidas** (lista exata do README, mais as regras do pitch, e regex em `CONTENT.md`): "o código está correto", "trustless" ou "ninguém precisa confiar em ninguém", "qualquer repositório", "Verifier Router" como caminho atual, "mainnet" ou "dinheiro real" como capacidade, "ZK on-chain" sem a F1, "auditado", "privado", "máquina nova", e também "seguro", "garantido", "certificado", "agente verificado", "reputação", "pontuação", "nível de confiança" e "aprovado" como veredito.

### 2.2 Dados

- Todo número, endereço, hash e link de transação vem de `facts.json`. **Nenhum valor digitado à mão** em componente ou texto.
- Nunca invente: clientes, parceiros, apoiadores, prêmios, depoimentos, métricas de uso, integrantes da equipe, e-mails, URLs.
- Valor que falta (`null` em `facts.json` → `todo`: vídeos, e-mail, equipe, validação, modelo de negócio): **não coloque placeholder falso**. Oculte o elemento e registre a pendência no código e na lista final, com os mesmos marcadores da equipe do MVP: `TODO(video)`, `TODO(team)`, `TODO(validation)`, `TODO(business)`, `TODO(brand)`, `TODO(repo)`. (A exceção é a validação: sem dados, a página diz "No user validation yet.")
- Nada de logotipos de terceiros (Solana, RISC Zero, Colosseum, universidades, aceleradoras) que sugiram endosso. Use **texto**. Se o dono aprovar logotipos, use somente os arquivos oficiais, respeitando as diretrizes de marca de cada um.

### 2.3 Nomenclatura (Hive e VeriCode)

- O produto se chama **Hive**. O código, os programas, a CLI e o repositório mantêm o nome legado **VeriCode** e **isso não muda**.
- Em títulos, textos institucionais, `<title>`, metadados e logotipo, a marca é **Hive**.
- Identificadores técnicos exibidos (comando da CLI `vericode`, programa `vericode_escrow`, nomes de erro, endereços) aparecem **exatamente como existem**. Não traduza nem "corrija".
- Inclua a nota da seção "Verify it yourself": no repositório, os nomes de código mantêm o nome original, VeriCode.

### 2.4 Privacidade

Sem cookies, sem analytics, sem scripts de terceiros, sem formulário de e-mail. O vídeo é carregado **só após clique** (veja 8.4). A página declara isso no rodapé.

## 3. Referência de design: usebido.com

O dono pediu que a página **siga o design de https://www.usebido.com/**. A regra de ouro:

> **Estrutura, ritmo e padrões de seção vêm do Bido. Paleta, tipografia, logotipo, formas e textos vêm da Hive. Em caso de conflito, a identidade da Hive vence.**

Estude, não clone: não copie código, textos, imagens, vídeos, logotipos nem a faixa de "apoiadores" do Bido.

### 3.1 O que o Bido faz (observado na página em 2026-10-09)

Barra de aviso no topo; navegação flutuante com logotipo, três âncoras, alternância de idioma (PT-BR e EN) e botão de ação; hero em tela cheia com vídeo de fundo, rótulo, título grande, parágrafo e uma chamada à ação; faixa de logotipos de apoiadores; seção com título e **três passos numerados**, cada um com título, parágrafo, uma linha de etiquetas em minúsculas separadas por pontos e um **cartão que simula a interface do produto** (o terceiro passo leva a etiqueta **ROADMAP**); seção de "canais" com título em dois tons, parágrafo e três colunas com imagens; chamada final; rodapé em colunas com contato e links legais.

### 3.2 Mapeamento Bido → Hive

| Bido | Hive | Observação |
| --- | --- | --- |
| Barra de aviso ("pilot partners") | "Built for the Colosseum Hackathon. Running on Solana devnet." + link para o vídeo (ou, sem vídeo, para o repositório) | **Não** diga que há parceiros piloto |
| Navegação flutuante, âncoras, PT-BR/EN, botão | Logotipo horizontal, 4 âncoras, alternância EN/PT-BR, botão "Watch the demo" | Alternância por **links** (veja seção 7) |
| Hero com vídeo de fundo e e-mail | Hero em **berinjela**, título, subtítulo, F1 com o link, **cartão de liquidação gravada**, dois botões | Sem vídeo de fundo, sem campo de e-mail |
| Faixa "Backed, trained and awarded by" | Faixa "Built with": **texto** (Solana devnet, RISC Zero, Anchor, verificador Groth16) | Nada de apoiadores |
| (não há) | "The problem" e "Who it is for", curtas, antes dos passos | Textos do pitch e da submissão |
| 3 passos numerados com cartão de produto | **4 passos reais** (create and fund, prove locally, deliver and settle, timeout) + um bloco **Roadmap (not built yet)**, cada passo com **cartão de execução gravada** | Cartões usam `facts.json`; o 3º passo do Bido também leva etiqueta de roadmap |
| Seção "Omnichannel" (3 canais) | "Verify it yourself": **Explorer**, **CLI**, **interface Hive** | Cada coluna com link ou comando reais |
| (não há) | "What the program refuses": 4 rejeições reais | É a prova mais forte do MVP |
| (não há) | "What this shows, and what it doesn't" | Limites declarados |
| Chamada final | Slogan oficial + 3 botões | Slogan verbatim |
| Rodapé em colunas | Produto, Projeto, Contato + declaração de privacidade | Páginas legais só se houver coleta de dados (não há) |

### 3.3 Procedimento de estudo (obrigatório na Etapa 0 do plano)

1. Abra o site de referência no navegador. Capture telas em **1440 px** e **390 px** de largura.
2. Registre em `docs/reference-notes.md`: largura do contêiner, espaçamento vertical entre seções, escala de títulos, raios, sombras, estilo dos cartões, comportamento da navegação (fixa, transparente sobre o hero, mudança de estado ao rolar), animações de entrada.
3. **Traduza** cada observação para os tokens da Hive (seção 5). Registre também o que você **descartou** por conflitar com a identidade.

O que está estabelecido sem inspeção: a ordem das seções (3.1) e o tema geral de cores claras com hero escuro. O resto (tipografia, espaçamentos, efeitos) você precisa observar; não presuma.

## 4. Identidade Hive (resumo operacional)

Fonte: documento de identidade de 05.10.2026. **Os valores abaixo não podem ser alterados.** Personalidade: serena, precisa, criteriosa, cooperativa.

### 4.1 Cores

| Token | Hex | Uso |
| --- | --- | --- |
| `--hive-aubergine` | `#392D40` | Identidade, hero, rodapé, títulos e texto principal sobre fundo claro |
| `--hive-amber` | `#E8B44C` | Ação principal, foco/seleção, detalhes; **texto/ícone só sobre berinjela** |
| `--hive-warm-white` | `#FAF7F5` | Fundo geral da página |
| `--hive-lilac` | `#E7DFE9` | Superfícies secundárias, divisórias, texto secundário **sobre berinjela** |
| `--hive-mauve` | `#796680` | Texto secundário **sobre fundo claro** |
| `--hive-white` | `#FFFFFF` | Cartões e painéis claros |
| `--hive-on-amber` | `#392D40` | Texto sobre botão âmbar |

Derivados para acessibilidade (não vêm da identidade): `--hive-border-strong: #9B8AA2` (borda de campo/controle, 3,2:1 sobre branco); foco: `#392D40` sobre fundo claro e `#E8B44C` sobre berinjela.

Status (propostos, usados nos cartões; sempre com ícone e rótulo): sucesso `#1B6B43` sobre `#E3F1E8`; erro `#A8281F` sobre `#FBE7E4`; atenção `#7A4B00` sobre `#F9EBD0`; neutro `#5E4B66` sobre `#E7DFE9`.

### 4.2 Regras de contraste (medidas)

| Combinação | Razão | Pode? |
| --- | --- | --- |
| Berinjela sobre branco quente | 12,1 | Sim (texto) |
| Branco quente / lilás sobre berinjela | 12,1 / 9,9 | Sim (texto) |
| Âmbar sobre berinjela | 6,8 | Sim (texto, link, ícone) |
| Berinjela sobre âmbar | 6,8 | Sim (botão primário) |
| Malva sobre branco quente / branco | 4,9 / 5,2 | Sim (texto secundário) |
| **Malva sobre lilás** | **4,0** | **Não** (use berinjela) |
| **Malva sobre berinjela** | **2,5** | **Não** (use lilás) |
| **Âmbar sobre branco quente ou branco** | **1,8** | **Não** (nem texto, nem foco, nem ícone informativo) |

### 4.3 Uso do âmbar

Ação principal, foco e detalhes. **Nunca** como cor de resultado, aprovação ou "sucesso". Evite áreas grandes preenchidas. No máximo **um botão primário por bloco**. Hover: misture o âmbar com 12% de berinjela (`color-mix`), sem inventar hex novo.

### 4.4 Tipografia

- **Manrope** (variável, 200 a 800) para tudo, exceto conteúdo técnico. **IBM Plex Mono** (400) só para hashes, endereços, assinaturas, comandos, nomes de erro, versões, IDs.
- **Auto-hospede** as fontes (`@fontsource-variable/manrope`, `@fontsource/ibm-plex-mono`), subconjunto latino, `font-display: swap`, pré-carregue a Manrope.
- Nem a Manrope nem a IBM Plex Mono têm os caracteres `→` e `≈`. **Não os use no texto.** Use ícone SVG para setas e `~` para estimativas.
- Números com `font-variant-numeric: tabular-nums`. Sinal de menos tipográfico `−` (U+2212).

Escala (a de "Título de destaque" e corpo vem da identidade; a de seção foi **adaptada** para landing):

| Papel | Desktop / celular | Peso |
| --- | --- | --- |
| Título do hero (identidade) | 56 / 36 px, entrelinha 1,1 | 700 |
| Título de seção (adaptado) | 40 / 28 px, entrelinha 1,15 | 600 |
| Título de cartão (identidade, H3) | 20 / 18 px | 600 |
| Parágrafo de abertura | 20 / 17 px, entrelinha 1,5 | 400 |
| Corpo (identidade) | 16 px / 24 px | 400 |
| Rótulo e etiqueta | 13–14 px | 500–600 |
| Dado técnico (mono) | 13–14 px | 400 |
| Legenda | 12–14 px | 400 |

Caixa de frase em títulos e botões. Nada de títulos em caixa alta com espaçamento largo. Largura de leitura de 60 a 75 caracteres.

### 4.5 Forma, profundidade e movimento

- Botões e campos com raio de **8 px**; cartões com **12 px**. Cápsulas só para chips pequenos (ambiente, etiquetas). Nada de botões 100% arredondados só porque o Bido os usa.
- Bordas de 1 px e tons de superfície em vez de sombras. No máximo **uma** sombra suave para elementos elevados (menu, popover). Sem brilho, degradê decorativo, relevo ou desfoque de fundo.
- Traço de espessura uniforme. **Nunca** varie espessura, tamanho ou cor para sugerir confiança ou pontuação.
- Movimento só para mostrar mudança real: revelar seção ao rolar (opacidade + 8 px, 300 ms), foco, confirmação de cópia, troca de idioma. `prefers-reduced-motion: reduce` desliga tudo que não seja essencial.
- Ícones: um único conjunto de linha, traço de 1,5 px (ex.: `lucide-static`, licença ISC). Ícone de estado sempre com texto.

### 4.6 Elementos da marca: o que entra e o que não entra

| Elemento | Na landing |
| --- | --- |
| Logotipo horizontal, símbolo, wordmark | Sim, **só os SVGs fornecidos** (seção 9) |
| Hexágono (célula, ponto para cima, cantos levemente arredondados) | Sim, com contenção: ilustra **partes** (comprador e executor). **Idêntico em PASS e em FAIL.** |
| Linha com seta e ponto percorrendo | Sim, para mostrar a delegação, se houver tempo |
| Halo de confiança, selos, escudos, pontuação, "níveis de confiança" | **Não.** O MVP não produz perfis contextuais |
| Padrão de favos como fundo | **Não** (compete com os dados e dá ar decorativo) |
| Mascote | Não é necessário. Se o dono pedir, uma vez só, longe das seções de prova |
| Qualquer visual de rede ou "colmeia" | Somente dentro do bloco **Roadmap (not built yet)**, com a etiqueta |

## 5. Tokens (um único lugar)

Todo valor visual vive em `src/styles/tokens.css` como variáveis `--hive-*`. Componentes **só leem variáveis**. Nada de hex, px de fonte ou raio literal em componente. Trocar a identidade deve exigir mexer em um arquivo.

Variáveis mínimas: cores (4.1), `--hive-font-sans`, `--hive-font-mono`, escala tipográfica (4.4), raios (8 e 12 px), espaçamentos de base 4 px (`4, 8, 12, 16, 24, 32, 48, 64, 96, 128`), `--hive-container: 1200px`, `--hive-section-y: 128px` desktop e `72px` celular, durações de movimento (`120ms`, `200ms`, `300ms`).

## 6. Estrutura da página (ordem fixa)

Âncora entre parênteses. O detalhe de cada seção, com dados e links, está no `PLAN.md`.

1. Barra de aviso
2. Navegação flutuante
3. Hero (`#top`)
4. Faixa "Built with"
5. "The problem" e "Who it is for" (curtas)
6. "How it works": 4 passos + bloco Roadmap (`#how`)
7. "What the program refuses" (`#proof`)
8. Vídeo da demonstração (`#demo`)
9. "Verify it yourself" (`#verify`)
10. "Under the hood" (arquitetura)
11. "What this shows, and what it doesn't" (`#limits`)
12. Equipe e contato (**só se os dados forem fornecidos**)
13. FAQ curta (opcional; primeira a ser cortada)
14. Chamada final com o slogan oficial
15. Rodapé

## 7. Idiomas (inglês e português)

- Locales: `en` (**padrão**, a submissão é em inglês) e `pt-BR`.
- Rotas: `/` em inglês e `/pt/` em português. **Não redirecione** por idioma do navegador. A alternância é um **link** para a página equivalente, preservando a âncora (`/#proof` ↔ `/pt/#proof`).
- `<html lang="en">` e `<html lang="pt-BR">`; `<link rel="alternate" hreflang>` para os dois e `x-default` para o inglês; título e descrição traduzidos.
- **Nenhum texto fixo em componente.** Tudo em `src/i18n/en.json` e `src/i18n/pt-br.json`, com as mesmas chaves. Crie `scripts/check-i18n.mjs` que **falha o build** se faltar chave em algum idioma ou sobrar uma.
- **Não traduza**: endereços, hashes, comandos, nomes de programa, nomes e códigos de erro, nomes de estado (`Funded`, `Released`, `RefundedOnFail`, `RefundedOnTimeout`, `PASS`, `FAIL`), `VeriCode`.
- Formatos por idioma: `99,541 CU` (EN) e `99.541 CU` (PT-BR), via `Intl.NumberFormat`. O inglês é a versão canônica dos claims; o português é tradução fiel, **sem acrescentar nem tirar nada**.
- Textos marcados `status: draft` em `CONTENT.md` aguardam aprovação do dono. Use-os, mas liste-os no relatório final.

## 8. Stack, qualidade e entrega

### 8.1 Stack

Se o repositório da landing já tiver stack definida, **mantenha-a**. Caso contrário, recomendação: **Astro** (saída estática, roteamento de idiomas nativo, JavaScript mínimo), **CSS puro** com os tokens, sem framework de UI, sem biblioteca de animação. Dependências de desenvolvimento permitidas: `@fontsource-variable/manrope`, `@fontsource/ibm-plex-mono`, `lucide-static`, `playwright` (capturas e QA). Hospedagem estática (Vercel, Netlify, Cloudflare Pages ou GitHub Pages).

### 8.2 Estrutura de pastas

```
.
├── AGENTS.md  CONTENT.md  PLAN.md  facts.json
├── docs/reference-notes.md
├── public/
│   ├── brand/            SVGs recebidos (nomes originais; não editar)
│   ├── og/               imagem social 1200×630
│   └── favicon.svg
├── scripts/              check-i18n.mjs, check-claims.mjs, check-links.mjs
└── src/
    ├── data/facts.json   (cópia lida pelos componentes)
    ├── i18n/             en.json, pt-br.json
    ├── styles/           tokens.css, base.css
    ├── components/       um componente por seção
    └── pages/            index e pt/index
```

### 8.3 Qualidade mínima

- **Acessibilidade:** HTML semântico, um `h1` por página, ordem de títulos coerente, link "pular para o conteúdo", foco visível (4.1), alvos de toque de pelo menos 40 px, estado nunca só por cor, `alt` em imagens informativas, `aria-label` distinguindo **qual** valor cada botão de copiar copia.
- **Desempenho:** sem vídeo de fundo, sem bibliotecas pesadas; imagens em AVIF ou WebP com dimensões declaradas; fontes só latinas e pré-carregadas. Meta: Lighthouse **≥ 90** em Performance, Acessibilidade, Boas práticas e SEO, em desktop e celular.
- **Responsivo:** 390, 768, 1024, 1440 px sem rolagem horizontal. Hashes e endereços quebram com segurança, sem estourar o layout.
- **SEO e compartilhamento:** `title`, `description`, Open Graph e Twitter Card por idioma; imagem OG de 1200×630 gerada com a identidade (berinjela, logotipo horizontal branco, título). `lang` e `hreflang` corretos.
- **Links:** todo link do Explorer abre e mostra a transação ou conta no cluster **devnet**. `scripts/check-links.mjs` confere o formato; a conferência final dos links é manual (8.5).

### 8.4 Vídeo

Bloco de vídeo com **imagem de capa** e botão de reprodução; o `iframe` (versão sem cookies do provedor) só é inserido **após o clique**. Enquanto `facts.json` → `todo.technicalDemoUrl` (ou `todo.demoVideoUrl`) for `null`, mostre o bloco como "Demo video: coming soon" **ou oculte-o**, e troque os botões "Watch the demo" por "View the repository"; nunca um player quebrado.

### 8.5 Definição de pronto

Marque cada item e reporte:

1. Nenhum texto fora de `i18n`; `check-i18n` passa.
2. Nenhum número, endereço ou link digitado à mão; tudo vem de `facts.json`.
3. `check-claims` não encontra frase proibida (exceto as frases de "limites", revisadas manualmente).
4. O claim de verificação on-chain tem o link da liquidação `U6` ao lado, em **todas** as ocorrências, nos dois idiomas.
5. "Test USDC" e "devnet" aparecem em todo bloco que fala de dinheiro.
6. Todos os links de Explorer foram **abertos e conferidos** manualmente.
7. Contraste conferido nas combinações da tabela 4.2; foco visível; navegação por teclado completa.
8. Lighthouse ≥ 90 nas quatro categorias, em desktop e celular.
9. 390, 768, 1024 e 1440 px sem rolagem horizontal.
10. `prefers-reduced-motion` respeitado.
11. Trocar o idioma preserva a âncora; `hreflang` correto.
12. Nenhum logotipo de terceiros; nenhum apoiador, cliente, parceiro ou depoimento.
13. Os SVGs de marca estão como recebidos (sem edição, sem recolorir fora das variantes).
14. Lista final de `TODO(...)` e de textos `draft` entregue ao dono.
15. As frases F1 a F8 vêm de `facts.json` (nenhuma redigitada) e batem com o README do repositório do MVP.
16. Todo cartão de transação diz "Recorded run" e nomeia o Job; nada é apresentado como ao vivo.
17. `AGENTS.md` tem menos de 28 KB (o Codex carrega no máximo 32 KiB de instruções).

## 9. Assets de marca (SVG)

Os SVGs chegam do dono do projeto e ficam em `public/brand/` **com os nomes originais**. Os mesmos arquivos, byte a byte, estão no repositório do MVP (`brand/logo/` e `brand/symbol/`); se faltar algum, copie de lá. As fontes (Manrope e IBM Plex Mono, licença OFL) também estão lá, em `brand/fonts/`. Nomes esperados: `hive-horizontal-berinjela.svg`, `hive-horizontal-branco.svg`, `hive-horizontal-ambar.svg`, `hive-symbol.svg`, `hive-symbol-branco.svg`, `hive-symbol-ambar.svg`, `hive-wordmark-berinjela.svg`, `hive-wordmark-branco.svg`.

- **São provisórios** (rastreados da prancha de identidade; ainda não existe o desenho mestre). Use-os assim mesmo, por **um único componente** `BrandMark` que centraliza o caminho, para trocar pelo mestre mexendo em um ponto só. Marque `TODO(brand)`.
- **Nunca** redesenhe, trace, recolora fora das variantes, distorça, gire, espelhe, aplique sombra ou efeito, nem redigite "hive" com a fonte do site para imitar o logotipo.
- Sobre berinjela (hero, rodapé): `hive-horizontal-branco.svg`. Sobre fundo claro: `hive-horizontal-berinjela.svg`.
- Área de proteção: `x = H ÷ 4` ao redor da assinatura, onde `H` é a altura do símbolo. Mínimos propostos (a validar): horizontal 128 px de largura, símbolo 24 px de altura.
- **Favicon:** não existe arquivo oficial. É permitido **compor** (sem redesenhar) um quadrado berinjela com cantos arredondados contendo `hive-symbol-ambar.svg` a ~62% da largura. Marque `TODO(brand)` e informe o dono.
- Se faltar um arquivo, mostre um texto provisório marcado `TODO(brand)` e avise. Não improvise um desenho.

## 10. O que não fazer

- Não copiar o Bido (código, texto, imagem, vídeo, logotipo, "apoiadores").
- Não usar vídeo de fundo, pré-carregador em vídeo, campo de e-mail, cookies nem analytics.
- Não escrever claim novo, número novo, link novo nem nome de pessoa.
- Não usar âmbar sobre fundo claro como texto, foco ou ícone informativo.
- Não usar `→` ou `≈` como caracteres de texto.
- Não mostrar halo, selo, pontuação, favos de fundo ou "níveis de confiança".
- Não traduzir identificadores técnicos nem renomear `VeriCode` onde ele aparece.
- Não adicionar dependências sem necessidade clara.
- Não fazer commit, push ou deploy sem pedido do dono (a exceção é a Etapa 10 do plano, autorizada por ele).
