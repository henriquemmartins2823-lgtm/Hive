# CONTENT.md: claims, textos e vocabulário da landing da Hive

**Fonte dos fatos:** o repositório do MVP, <https://github.com/Lucas-Ibanez/colosseum-hackathon-sparta> (público, Apache-2.0; HEAD `b84461e`, 2026-10-08), mais o relatório de estado de 2026-10-07. Os números, endereços e links estão em `facts.json`, extraídos por script e conferidos entre as duas fontes. **Este arquivo não cria fatos.**

**Colunas "Fonte" nas tabelas de texto:**
- `README`: frase ratificada, copiada do `README.md` (EN) ou de `docs/README.pt-BR.md` (PT). Não alterar.
- `submission`: texto de `docs/submission.md` do repositório do MVP.
- `pitch`: texto de `docs/pitch-script.md`.
- `draft`: redação ou tradução minha, **pendente de aprovação do dono**. Use, mas liste no relatório final.

## 1. Claims congelados (F1 a F8)

Estas oito frases são as **únicas** afirmações sobre o que a Hive faz e prova. Estão copiadas, byte a byte, do repositório do MVP (`facts.json` → `claims.phrases`; o agente deve importar de lá, nunca redigitar). Mudá-las exige uma decisão registrada em `docs/decisions.md` **do repositório do MVP**, não na landing. Paráfrases são permitidas somente se **não disserem mais** do que a frase.

| # | Rótulo | English (ratificado) | Português (congelado) | Onde usar |
| --- | --- | --- | --- | --- |
| F1 | Claim | Hive's Groth16 receipt is verified on devnet via CPI to the immutable Groth16 verifier of risc0-solana v3.0.0, in the same instruction that releases or refunds the Job's Test USDC. | A receipt Groth16 da Hive é verificada em devnet por CPI ao verificador Groth16 imutável de risc0-solana v3.0.0, na mesma instrução que libera ou devolve o Test USDC do Job. | Hero e passo 3. **Sempre com o link `U6`** (ou outra transação da tabela do README) ao lado. |
| F2 | Statement | A previously committed deterministic evaluator ran on the artifact delivered in the Job and produced the published verdict. The program moves the Test USDC only after checking the binding between journal, Job and delivery and verifying the proof. | Um avaliador determinístico previamente comprometido executou sobre o artefato entregue no Job e produziu o veredito publicado. O programa só move o Test USDC depois de conferir o vínculo entre journal, Job e entrega e de verificar a prova. | "What this shows". Pode inspirar a introdução de "How it works", sem acrescentar nada. |
| F3 | Limit | The proof attests to the execution of the fixed rule on this artifact, not to the quality of a piece of software. The v1 rule is trivial (output = 2 × input) and serves to demonstrate the flow. | A prova atesta a execução da regra fixa sobre este artefato, não a qualidade de um software. A regra v1 é trivial (saída = 2 × entrada) e serve para demonstrar o fluxo. | "What this doesn't show". **Obrigatória.** |
| F4 | No administrator | The escrow and the verifier are immutable (upgrade authority `none`). No one, not even the project, changes the rules or decides the payment; there is also no e-stop. | O escrow e o verificador são imutáveis (upgrade authority `none`). Ninguém, nem o projeto, muda as regras ou decide o pagamento; também não existe e-stop. | "Verify it yourself" e "What this shows". |
| F5 | Network | Devnet and Test USDC only; none of this exists on mainnet. | Só devnet e Test USDC; nada disso existe em mainnet. | Barra de aviso, microtexto do hero e limites. |
| F6 | Negatives | On devnet, a tampered proof, a journal from another Job, a refund before the deadline and a second settlement were rejected without moving funds. | Em devnet, uma prova adulterada, um journal de outro Job, um reembolso antes do prazo e uma segunda liquidação foram rejeitados sem mover fundos. | Legenda de "What the program refuses". **Sempre com os links.** |
| F7 | Reproduction | The flow was reproduced with this repository's CLI and prover in a clean environment: a fresh clone and fresh targets, with copied isolated toolchains, not a new machine. | O fluxo foi reproduzido pela CLI e pelo prover deste repositório num ambiente limpo: clone e targets novos, com toolchains isoladas copiadas, não uma máquina nova. | "What this shows" (opcional). ((D9)) |
| F8 | Proof | The proof is generated locally and compressed to Groth16 in a local Docker container, with no network access. | A prova é gerada localmente e comprimida para Groth16 num container Docker local, sem rede. | Passo 2 e "What this shows". |

**"Do not say" (README, ratificado):**

- EN: "the code is correct"; "trustless" or "nobody needs to trust anybody"; "any repository"; "Verifier Router" as the current path; "mainnet" or "real money"; "ZK on-chain" without phrase 1; "audited", "private" or "new machine". Also do not present an earlier run as live, nor show a receipt without saying which Job it belongs to.
- PT: "o código está correto"; "trustless" ou "ninguém precisa confiar em ninguém"; "qualquer repositório"; "Verifier Router" como caminho atual; "mainnet" ou "dinheiro real"; "ZK on-chain" sem a frase 1; "auditado"; "privado"; "máquina nova". Também não apresentar uma execução anterior como ao vivo, nem mostrar uma receipt sem dizer de qual Job ela é.

**Regras adicionais da equipe do MVP (pitch e vídeos), que a landing também segue:**

- Nunca apresentar uma execução anterior como se fosse **ao vivo**. Todo dado de transação na página é de uma **execução gravada** em devnet: rotule cada cartão com "Recorded run" / "Execução gravada" e a data (2026-10-07, rodada D11–D12).
- Nunca mostrar uma receipt, um estado ou uma transação **sem dizer de qual Job** ela é (por exemplo, "Job P₃ `26df9ef4…`").
- Não usar "secure", "safe", "guaranteed", "certified", "verified agent", "reputation", "score", "trust level" nem "approved" como veredito (PT: "seguro", "garantido", "certificado", "agente verificado", "reputação", "pontuação", "nível de confiança", "aprovado").
- Tudo o que não foi construído é dito como futuro ("next", "we plan to", "roadmap") e fica sob a etiqueta **Roadmap (not built yet)**.
- Nada sobre equipe, usuários, validação, parceiros, números ou modelo de negócio que a equipe não tenha fornecido. Lacuna sem dado: oculte o elemento ou, no caso da validação, diga "No user validation yet."

## 2. Varredura automática

`scripts/check-claims.mjs` varre o HTML gerado, nos dois idiomas, e **sinaliza** ocorrências. Ocorrências legítimas, que **negam** o termo (por exemplo, "none of this exists on mainnet" nos limites ou no FAQ, ou "No Verifier Router" nos limites), levam `data-claims-allow="negation"` e são revisadas à mão.

```
EN: trustless|nobody needs to trust|guarantee|audited|\bprivate\b|mainnet|real money|any repo|correct code|code is correct|verifier router|zk[- ]?on-?chain|(fresh|new) machine|\bsecure\b|\bsafe\b|certified|(trusted|verified) agent|reputation|\bscore\b|trust level|\bapproved\b|pilot partner|customers|backed by
PT: trustless|ninguém precisa confiar|garant(ido|ia|e)|auditad|privad|mainnet|dinheiro real|qualquer reposit[óo]rio|código (está )?correto|verifier router|zk[- ]?on-?chain|máquina nova|\bseguro\b|certificad|agente (confiável|verificado)|reputaç|pontuaç|nível de confiança|\baprovado\b|parceiros? piloto|clientes|apoiad
```

Observações: "mainnet" e "Verifier Router" só aparecem na seção de limites, em frases que **negam** (F5; "no Verifier Router"). "ZK on-chain" e "verified on-chain" só aparecem dentro da F1 completa, com o link.

## 3. Vocabulário

| Use | Evite |
| --- | --- |
| buyer / comprador, executor, Job, artifact / artefato, proof / prova, receipt, verdict / veredito | "worker" no texto de marketing (é componente interno), "agent" como se o produto já tivesse agentes autônomos |
| "releases" / "libera", "refunds" / "reembolsa" ou "devolve", "returns" | "pays out", "rewards" |
| "verifies" / "verifica", "checks the binding" / "confere o vínculo" | "validates", "approves", "certifies" |
| "Test USDC on Solana devnet" | "USDC", "crypto", "tokens" soltos |
| `Funded`, `Released`, `RefundedOnFail`, `RefundedOnTimeout`, `PASS`, `FAIL` (em mono, sem traduzir) | traduzir nomes de estado |

Tom: sereno, curioso, criterioso. Frases curtas, afirmações verificáveis, sem exclamações nem superlativos.

## 4. Textos por seção

Chaves sugeridas para `i18n`. Onde houver número, endereço ou link, o componente lê `facts.json`; o texto abaixo é só a moldura.

### 4.1 Metadados

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `meta.title` | Hive: escrow released by proof, not by promise | Hive: escrow liberado por prova, não por promessa | draft |
| `meta.description` | Hive is an escrow for development tasks between agents, released after deterministic verification and a zkVM proof, on Solana devnet. | A Hive é um escrow para tarefas de desenvolvimento entre agentes, liberado após verificação determinística e uma prova zkVM, na devnet da Solana. | submission (one-liner) + draft PT |
| `meta.og.title` | Hive. Trust starts with a reason. | Hive. Confiança começa com um porquê. | identidade |

### 4.2 Barra de aviso e navegação

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `announce.text` | Built for the Colosseum Hackathon. Running on Solana devnet. | Feito para o Hackathon da Colosseum. Rodando na devnet da Solana. | draft |
| `announce.cta` | Watch the demo | Ver a demo | draft |
| `nav.how` | How it works | Como funciona | draft |
| `nav.proof` | Proof | Prova | draft |
| `nav.verify` | Verify | Verificar | draft |
| `nav.limits` | Limits | Limites | draft |
| `nav.cta` | Watch the demo | Ver a demo | draft |

**Regra do vídeo:** enquanto `todo.demoVideoUrl` (ou `todo.technicalDemoUrl`) for `null`, os botões "Watch the demo" **não aparecem**; no lugar deles use "View the repository" / "Ver o repositório" (`repo.url`).

### 4.3 Hero

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `hero.eyebrow` | Agent trust and verification | Confiança e verificação entre agentes | identidade (posicionamento) |
| `hero.title` | Payment released by proof, not by promise. | Pagamento liberado por prova, não por promessa. | draft |
| `hero.lead` | Hive is an escrow for development tasks between agents. The acceptance criteria are fixed before any work starts, and the payment moves only after a zkVM proof is verified, on Solana devnet. | A Hive é um escrow para tarefas de desenvolvimento entre agentes. Os critérios de aceitação são fixados antes de qualquer trabalho, e o pagamento só se move depois que uma prova zkVM é verificada, na devnet da Solana. | submission + draft PT |
| `hero.claim` | **F1 completa**, com o link `U6` imediatamente ao lado | idem (F1 em português) | README |
| `hero.cta.primary` | Watch the demo | Ver a demo | draft |
| `hero.cta.secondary` | See a real settlement | Ver uma liquidação real | draft |
| `hero.micro` | Recorded runs on Solana devnet. Test USDC, no real funds. | Execuções gravadas na devnet da Solana. Test USDC, sem fundos reais. | draft |

Por que este título: "provado" prometeria qualidade do trabalho, e a F3 diz que a prova **não** atesta isso. "Liberado por prova" descreve o mecanismo (F2).

**Cartão do hero** ("settlement card"; `facts.json` → `uiRound.transactions`, `U6`): selo "Recorded run, 2026-10-07" e "Job P₃ `26df9ef4…`"; estado `Released`; "1 Test USDC to the executor / ao executor"; "122,156 CU total, 99,541 CU in the verifier / no verificador"; link "View on Explorer / Ver no Explorer". Selo "Solana devnet".

### 4.4 Faixa "Built with"

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `built.label` | Built with | Construído com | draft |
| `built.items` | Solana devnet, RISC Zero 3.0.3, Anchor 0.31.1, Groth16 verifier from risc0-solana v3.0.0 | Solana devnet, RISC Zero 3.0.3, Anchor 0.31.1, verificador Groth16 do risc0-solana v3.0.0 | README |

Apenas texto, sem logotipos. Renderize cada item separado por espaçamento, sem ponto médio nem seta.

### 4.5 O problema e para quem é

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `problem.title` | When an AI agent delivers work, who decides whether it gets paid? | Quando um agente de IA entrega um trabalho, quem decide se ele é pago? | pitch (slide 2) + draft PT |
| `problem.body` | AI coding agents are starting to take on delegated development tasks. Today, someone reviews the delivery by hand, or both sides rely on the platform in the middle to decide. The payment depends on a judgment that is hard to check afterwards. | Agentes de IA que programam começam a assumir tarefas de desenvolvimento delegadas. Hoje, alguém revisa a entrega à mão, ou as duas partes dependem da plataforma do meio para decidir. O pagamento depende de um julgamento difícil de conferir depois. | pitch + draft PT |
| `for.title` | Who it is for | Para quem é | pitch |
| `for.body` | We are building for tech leads and partners at AI-native software houses that hand tasks to agents, and for operators of job platforms that pay for delegated work. They have bounded tasks, acceptance criteria that can be automated, and distinct parties on each side. | Estamos construindo para tech leads e sócios de software houses nativas de IA que delegam tarefas a agentes, e para operadores de plataformas de jobs que pagam por trabalho delegado. Eles têm tarefas delimitadas, critérios de aceitação automatizáveis e partes distintas de cada lado. | pitch + draft PT |
| `for.validation` | No user validation yet. Next, we plan to put this flow in front of design partners. | Ainda não há validação com usuários. Em seguida, planejamos colocar este fluxo diante de design partners. | pitch + draft PT |

`for.validation` aparece **somente** enquanto `todo.validation` for `null`. Se a equipe fornecer validação real, troque por ela.

### 4.6 "How it works"

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `how.eyebrow` | From task to settlement | Da tarefa à liquidação | draft |
| `how.title` | One Job, from funding to settlement. | Um Job, do financiamento à liquidação. | draft |

Quatro passos reais (README, "How it works"), mais um bloco de roadmap. Cada passo: número, título, parágrafo, linha de etiquetas em minúsculas, cartão de **execução gravada**.

| Passo | English | Português | Fonte |
| --- | --- | --- | --- |
| `how.1.title` | Create and fund | Crie e financie | README |
| `how.1.body` | The buyer creates and funds the Job in a single transaction. The Job fixes the executor, the Test USDC mint, the amount, the deadline slot and the v1 terms. The vault is a token account whose authority is the Job's PDA. | O comprador cria e financia o Job numa só transação. O Job fixa o executor, o mint do Test USDC, o valor, o slot do prazo e os termos v1. O vault é uma conta de token cuja autoridade é a PDA do Job. | README + draft PT |
| `how.1.tags` | before the work, fixed terms, vault, deadline | antes do trabalho, termos fixos, vault, prazo | draft |
| `how.1.card` | Recorded run. Job P₃ `26df9ef4…`, `Funded`, 1 Test USDC, deadline 9,000 slots. Link: `U3`. | Execução gravada. Job P₃ `26df9ef4…`, `Funded`, 1 Test USDC, prazo de 9.000 slots. Link: `U3`. | facts |
| `how.2.title` | Prove locally | Prove localmente | README |
| `how.2.body` | The executor runs a RISC Zero guest that evaluates the artifact and publishes a 165-byte journal with the verdict, PASS or FAIL. The receipt is compressed to Groth16 in a local Docker container, with no network access. | O executor roda um guest RISC Zero que avalia o artefato e publica um journal de 165 bytes com o veredito, PASS ou FAIL. A receipt é comprimida para Groth16 num container Docker local, sem acesso à rede. | README (F8) + draft PT |
| `how.2.tags` | during the work, local proof, Composite then Groth16, verdict | durante o trabalho, prova local, Composite depois Groth16, veredito | draft |
| `how.2.card` | Recorded run. Job P₃, input `(21, 42)`, Composite 7.2 s, Groth16 177.9 s, verdict `PASS`. Label: "Generated locally, off-chain". | Execução gravada. Job P₃, entrada `(21, 42)`, Composite 7,2 s, Groth16 177,9 s, veredito `PASS`. Rótulo: "Gerada localmente, fora da cadeia". | facts |
| `how.3.title` | Deliver and settle | Entregue e liquide | README |
| `how.3.body` | In one transaction, the escrow checks the journal against the Job and the delivery, calls the immutable Groth16 verifier by CPI and moves the Test USDC: to the executor on PASS, back to the buyer on FAIL. Any mismatch or failed verification reverts the whole transaction. | Numa só transação, o escrow confere o journal contra o Job e a entrega, chama o verificador Groth16 imutável por CPI e move o Test USDC: ao executor no PASS, de volta ao comprador no FAIL. Qualquer divergência ou falha de verificação reverte a transação inteira. | README + draft PT |
| `how.3.tags` | settlement, verifier CPI, release or refund | liquidação, CPI ao verificador, liberação ou reembolso | draft |
| `how.3.card` | Recorded runs. Job P₃: `Released`, 1 Test USDC to the executor, 122,156 CU total, 99,541 CU in the verifier (`U6`). Job F₃ `7395a76d…`: `RefundedOnFail` (`U9`). | Execuções gravadas. Job P₃: `Released`, 1 Test USDC ao executor, 122.156 CU no total, 99.541 CU no verificador (`U6`). Job F₃ `7395a76d…`: `RefundedOnFail` (`U9`). | facts |
| `how.4.title` | Timeout | Prazo | README |
| `how.4.body` | After the deadline slot, anyone can call `refund_on_timeout`, and the Test USDC goes back to the buyer. | Depois do slot do prazo, qualquer um pode chamar `refund_on_timeout`, e o Test USDC volta ao comprador. | README + draft PT |
| `how.4.card` | Recorded run. Job T₃ `2c38ca66…`: `RefundedOnTimeout`, no verifier involved (`U10`). | Execução gravada. Job T₃ `2c38ca66…`: `RefundedOnTimeout`, sem verificador (`U10`). | facts |

**Bloco de roadmap** (etiqueta **Roadmap (not built yet)** / **Roadmap (ainda não construído)**; sem cartão de dados):

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `roadmap.title` | Next | Em seguida | draft |
| `roadmap.body` | Next, we plan to replace the trivial v1 rule with deterministic evaluators for real, bounded tasks, still on restricted artifacts. We also plan pilots that compare this zkVM evidence with simpler mechanisms, such as signed CI and human review, to learn how much evidence each kind of task needs. | Em seguida, planejamos trocar a regra v1 trivial por avaliadores determinísticos para tarefas reais e delimitadas, ainda sobre artefatos restritos. Também planejamos pilotos que comparam esta evidência zkVM com mecanismos mais simples, como CI assinado e revisão humana, para aprender quanta evidência cada tipo de tarefa exige. | pitch + draft PT |
| `roadmap.brand` (opcional) | Over time, verified interactions can build contextual trust. | Com o tempo, interações verificadas podem construir confiança contextual. | identidade (draft) |

Ilustração opcional: duas células hexagonais ligadas por uma linha com seta e o rótulo da tarefa, **idênticas em qualquer resultado**, sempre com a etiqueta de roadmap. Sem halo, favos, pontuação.

### 4.7 "What the program refuses"

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `proof.title` | What the program refuses. | O que o programa recusa. | draft |
| `proof.lead` | **F6**, como legenda, com os quatro links abaixo | idem (F6 em português) | README |
| `proof.note` | The Job's state was not changed. | O estado do Job não foi alterado. | draft (da interface) |

Quatro cartões (`facts.json`, `kind: "negative"`), cada um com **o Job**, o título, o nome do erro em mono, o código, quem rejeitou e o link:

| Cartão | English | Português | Erro | Rejeitou | Tx |
| --- | --- | --- | --- | --- | --- |
| 1 | Refund before the deadline (Job T₃) | Reembolso antes do prazo (Job T₃) | `DeadlineNotReached` 6021 | escrow | `U2` |
| 2 | Receipt of another Job (`bc334093…`) sent to Job P₃ | Receipt de outro Job (`bc334093…`) enviada ao Job P₃ | `JournalJobIdMismatch` 6014 | escrow | `U4` |
| 3 | Tampered proof (Job P₃) | Prova adulterada (Job P₃) | `PairingError` 6003 | verifier / verificador | `U5` |
| 4 | Second settlement (Job P₃) | Segunda liquidação (Job P₃) | `AlreadyReleased` 6007 | escrow | `U7` |

### 4.8 Demonstração em vídeo

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `demo.title` | See one Job run end to end. | Veja um Job rodar de ponta a ponta. | draft |
| `demo.lead` | A technical demo through the Hive interface, on Solana devnet. | Uma demo técnica pela interface da Hive, na devnet da Solana. | draft |
| `demo.soon` | Demo video coming soon. | Vídeo da demo em breve. | draft |

Há três vídeos planejados (`TODO(video)`): o **pitch** (até 3 min), a **demo técnica** (2 a 3 min, um corte rotulado da tomada contínua) e a **tomada contínua** sem cortes (~13 min). A landing destaca a **demo técnica** (`todo.technicalDemoUrl`) e, se existirem, oferece os outros dois como links secundários. O vídeo é em inglês; use a mesma URL nas duas versões da página.

### 4.9 "Verify it yourself"

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `verify.title` | Inspect it wherever you prefer. | Inspecione onde preferir. | draft |
| `verify.lead` | Every case above is recorded on Solana devnet, reproducible from the command line and visible in the Hive interface. | Cada caso acima está registrado na devnet da Solana, é reproduzível pela linha de comando e visível na interface da Hive. | draft |
| `verify.1.title` | On Solana Explorer | No Solana Explorer | draft |
| `verify.1.body` | Open the programs and the transactions. The escrow and the verifier are immutable: upgrade authority `none`. | Abra os programas e as transações. O escrow e o verificador são imutáveis: upgrade authority `none`. | README (F4) |
| `verify.2.title` | In the command line | Na linha de comando | draft |
| `verify.2.body` | Read a Job's state straight from the chain. Requires cloning the repository and building the CLI. | Leia o estado de um Job direto da cadeia. Exige clonar o repositório e compilar a CLI. | README + draft PT |
| `verify.3.title` | In the Hive interface | Na interface da Hive | draft |
| `verify.3.body` | Run the local worker and follow a Job from funding to settlement, with the proof timer, the local and on-chain checks and the transaction anatomy. There is no wallet in the browser. | Rode o worker local e acompanhe um Job do financiamento à liquidação, com o cronômetro da prova, as verificações local e on-chain e a anatomia da transação. Não há carteira no navegador. | README + draft PT |
| `verify.note` | In the repository, code names keep the original name, VeriCode. | No repositório, os nomes de código mantêm o nome original, VeriCode. | README |

- **Coluna 1:** endereços de `facts.json` (`programs.escrow`, `programs.verifier`, `mint`) com componente de hash (mono, cópia, valor completo) e o link da transação de finalização (`programs.escrow.finalizationTx`).
- **Coluna 2:** o comando **verbatim**, num bloco copiável, com um Job real de `facts.json` → `cliExamples.jobs` (Job P′, D9, `Released`): `vericode job show --job-id 91ea6fcdd2d0c29942246c664d893634b7c66f6cb2babbe436734a74bef5418e`. Link para a seção "Reproduce from a clone" do README (`repo.readme`).
- **Coluna 3:** "Runs locally on `127.0.0.1:8710/ui/`" e link para `worker/README.md` do repositório.
- **Mais evidências:** link para "All cases" (`repo.allCasesAnchor`; são 18 casos e 28 transações) e para `repo.evidence`.

### 4.10 "Under the hood"

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `hood.title` | Under the hood. | Por dentro. | draft |
| `hood.lead` | A fixed evaluator runs in a RISC Zero zkVM. The proof is verified by an immutable Groth16 verifier, through a call from the escrow program. | Um avaliador fixo roda numa zkVM RISC Zero. A prova é verificada por um verificador Groth16 imutável, por uma chamada do programa de escrow. | draft |

Diagrama simples em SVG (sem imagem importada): `Browser`, `local worker`, `CLI` e `Solana devnet`; do worker também o `prover` (Docker local, sem rede); na devnet, o `escrow program` chama por CPI o `Groth16 verifier` e o `SPL Token`. Rótulos de componente em mono. Ao lado, números de `facts.json`: 99,541 CU no verificador; prova Composite de 7 a 9 s; compressão Groth16 de 90 a 180 s; `JournalV1` de 165 bytes.

### 4.11 "What this shows, and what it doesn't"

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `limits.title` | What this shows, and what it doesn't. | O que isto demonstra, e o que não demonstra. | draft |
| `limits.shows` | What it shows | O que demonstra | draft |
| `limits.not` | What it doesn't show | O que não demonstra | draft |

- **Coluna "shows":** F2, F4, F6, F7 e F8.
- **Coluna "doesn't show":** F3 (**obrigatória**), F5 e as limitações abaixo.

| English | Português | Fonte |
| --- | --- | --- |
| No Verifier Router: the escrow calls the verifier directly, because the upstream Router on devnet is not initialized. | Sem Verifier Router: o escrow chama o verificador diretamente, porque o Router upstream da devnet não está inicializado. | README |
| No e-stop: a bug can only be fixed with a new program ID. | Sem e-stop: um bug só se corrige com um novo program ID. | README |
| The v1 rule is trivial, and the executor chooses the input: any `(n, 2n)` passes. | A regra v1 é trivial, e o executor escolhe a entrada: qualquer `(n, 2n)` passa. | README |
| No wallet in the browser: the local worker holds the project's devnet keys, and the same operator runs buyer and executor. | Sem carteira no navegador: o worker local guarda as chaves de devnet do projeto, e o mesmo operador faz comprador e executor. | README |
| The rent of each Job (about 0.0036 SOL) stays locked, because there is no `close`. | O rent de cada Job (cerca de 0,0036 SOL) fica preso, porque não há `close`. | README |
| The Test USDC mint authority is the project's deployer key. | A mint authority do Test USDC é a chave de deployer do projeto. | README |
| The Groth16 prover needs x86 Docker and a lot of memory. | O prover Groth16 exige Docker x86 e bastante memória. | README |

Esta seção torna crível o que foi provado: dê a ela o **mesmo peso visual** das demais.

### 4.12 Equipe e contato

Exibir **somente** com dados reais de `facts.json` → `todo.team` e `todo.contactEmail` (`TODO(team)`). Cada pessoa: nome, papel e um link. Sem dados, **oculte a seção** e liste a pendência. Há, porém, um link sempre disponível: o repositório (`repo.url`).

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `team.title` | The team | A equipe | draft |
| `contact.title` | Talk to us | Fale com a gente | draft |

### 4.13 FAQ (opcional; primeira a ser cortada)

| Pergunta (EN / PT) | Resposta (EN / PT) |
| --- | --- |
| Is this on mainnet? / Isto está na mainnet? | No. Devnet and Test USDC only; none of this exists on mainnet. (F5) / Não. Só devnet e Test USDC; nada disso existe em mainnet. (F5) |
| Does PASS mean the software is correct? / PASS significa que o software está correto? | No. The proof attests to the execution of the fixed rule on this artifact, not to the quality of a piece of software. (F3) / Não. A prova atesta a execução da regra fixa sobre este artefato, não a qualidade de um software. (F3) |
| Can anyone change the rules or decide the payment? / Alguém pode mudar as regras ou decidir o pagamento? | No. The escrow and the verifier are immutable (upgrade authority `none`), and there is no e-stop. (F4) / Não. O escrow e o verificador são imutáveis (upgrade authority `none`), e não existe e-stop. (F4) |
| Why does the repository say VeriCode? / Por que o repositório diz VeriCode? | Hive is the product's new name. The code, the programs and the command line keep the previous name. / Hive é o novo nome do produto. O código, os programas e a linha de comando mantêm o nome anterior. |
| Can I run it? / Posso rodar? | Yes, locally. It needs x86 Docker and enough memory for the prover. See "Reproduce from a clone" in the README. / Sim, localmente. Exige Docker x86 e memória suficiente para o prover. Veja "Reproduce from a clone" no README. |

### 4.14 Chamada final e rodapé

| Chave | English | Português | Fonte |
| --- | --- | --- | --- |
| `final.title` | Hive. Trust starts with a reason. | Hive. Confiança começa com um porquê. | identidade |
| `final.cta.demo` | Watch the demo | Ver a demo | draft (só com vídeo) |
| `final.cta.repo` | View the repository | Ver o repositório | draft |
| `final.cta.settlement` | See a real settlement | Ver uma liquidação real | draft |
| `footer.product` | Product | Produto | draft |
| `footer.project` | Project | Projeto | draft |
| `footer.contact` | Contact | Contato | draft |
| `footer.license` | Open source under the Apache-2.0 license. | Código aberto sob a licença Apache-2.0. | README |
| `footer.privacy` | This site uses no cookies and no analytics. | Este site não usa cookies nem analytics. | draft |
| `footer.legal` | Hackathon prototype on Solana devnet. No real funds. | Protótipo de hackathon na devnet da Solana. Sem fundos reais. | draft |

**Slogan:** usado **verbatim** ("Hive. Trust starts with a reason." / "Hive. Confiança começa com um porquê."), conforme o documento de identidade. O repositório do MVP ainda marca o slogan em inglês como `TODO(brand)`; a landing o usa como está na identidade e **lista isso como pendência de confirmação do dono**.
