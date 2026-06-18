# Elucidômetro — v1.0

Ferramenta web de **índice de solvabilidade investigativa** de homicídios dolosos. Estima, a partir das características registradas no momento do crime, a probabilidade histórica de elucidação de casos com perfil semelhante. Funciona inteiramente no navegador — **nenhum dado é enviado a servidores**.

> **A ferramenta informa, não decide.** Não mede eficácia investigativa, não avalia desempenho de equipes e **não** autoriza reduzir o esforço investigativo em nenhum caso. Ver a página *Governança & ética* na própria ferramenta.

Site: **www.elucidometro.com.br**

---

## O que a versão atual faz

- **Dois modelos**, na ordem de referência:
  - **INEH** — modelo completo (inclui todos os casos).
  - **IEIL** — métrica complementar, que exclui flagrantes e mortes por intervenção de agente do Estado.
- **Modelo real da tese embarcado** (DF, 2018–2023): coeficientes ajustados em Python (scikit-learn, regressão logística L2, C=0,1). Botão *"Carregar modelo real"* — INEH n=1342 (AUC 0,72) · IEIL n=1068 (AUC 0,71).
- **Upload de base própria (CSV)**: a ferramenta trata os dados automaticamente — reconhece/renomeia as colunas do questionário, deriva ano/mês/tempo de resposta a partir das datas, remove variáveis que vazam o resultado, normaliza o alvo (Sim/Não) e separa IEIL de INEH. O treino no navegador é uma **estimativa** (não idêntica ao scikit-learn).
- **Opção avançada — importar JSON**: carrega coeficientes já ajustados pelo pipeline oficial em Python, com **fidelidade total**.
- **Bases fictícias** para demonstração (dados sintéticos, não reais).
- **Elucidômetro interativo**: ajusta as características do caso e mostra a probabilidade estimada em tempo real.
- **Exportações**: HTML offline autossuficiente e especificação técnica em JSON.
- **Documentação & metodologia** e **Governança & ética** acessíveis por botões na própria ferramenta.

---

## Estrutura de publicação

O site é estático e composto pelos arquivos abaixo, todos na **raiz** do repositório:

```
index.html                → aplicação (interface + lógica)
support.js                → runtime que renderiza a aplicação
elucidometro_spec_v6.js   → modelo real da tese (coeficientes)
elucidometro_ingest.js    → tratamento automático das colunas do CSV
elucidometro_gov.js       → texto de governança e ética
CNAME                     → mantém o domínio elucidometro.com.br (NÃO remover)
.nojekyll                 → desliga o Jekyll do GitHub Pages (NÃO remover)
```

Os quatro `.js` precisam ficar **na mesma pasta** que o `index.html`. A aplicação só depende, externamente, das fontes do Google.

### Como atualizar a ferramenta

1. Obtenha os arquivos novos (apenas os que mudaram).
2. No repositório, **Add file → Upload files** e arraste os arquivos (substituem os de mesmo nome).
3. *Commit changes* (ex.: `Atualiza Elucidometro vX`).
4. Aguarde 1–3 min (GitHub Pages republica) e recarregue o site com Ctrl+F5.
5. **Não apague** os arquivos `CNAME` e `.nojekyll`.

---

## Privacidade e dados

- Todo o processamento (leitura do CSV, tratamento e cálculo) ocorre **localmente no navegador**.
- A ferramenta publica apenas **coeficientes** do modelo — nunca microdados ou registros de vítimas.

---

## Créditos e referência

- **Modelo e idealização:** Marcelo Zago.
- **Orientadores:** Felix Lopez (IPEA) e Franco Perazzoni (PF).

Referência da tese que originou o modelo:

> FERREIRA, Marcelo Zago Gomes. *Determinantes da eficácia investigativa em homicídios dolosos no Distrito Federal: uma análise multidimensional a partir do framework DOTS (2018–2023).* 2026. Tese (Doutorado Profissional em Administração Pública) — Instituto Brasileiro de Ensino, Desenvolvimento e Pesquisa (IDP), Brasília, 2026.

A documentação de governança, ética e limitações está embutida na ferramenta (botão *Governança & ética*) e é derivada das seções 8.2.5, 9.2, 9.3 e 9.4 da tese.

---

*Versão 1.0 — modelo de solvabilidade. Ferramenta de apoio à decisão investigativa.*
