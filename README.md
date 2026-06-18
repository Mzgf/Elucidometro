# Elucidômetro — v1.0

Ferramenta web de **índice de solvabilidade investigativa** de homicídios dolosos. Estima, a partir das características registradas no momento do crime, a probabilidade histórica de elucidação de casos com perfil semelhante.

> **A ferramenta informa, não decide.** Não mede eficácia investigativa, não avalia desempenho de equipes e **não** autoriza reduzir o esforço investigativo em nenhum caso. Ver a página *Governança & ética* na própria ferramenta.

Site: **www.elucidometro.com.br**

---

## Como o processamento funciona

A ferramenta tem dois caminhos, com tratamentos diferentes de privacidade:

- **Modelo oficial da tese** → roda em **servidor seguro** (Cloudflare Worker). O navegador envia apenas as **características do caso** (idade, sexo, meio empregado etc.) e recebe de volta **somente a probabilidade estimada**. Os **coeficientes do modelo permanecem no servidor** e não são transferidos para o navegador.
- **Bases próprias (CSV) e bases de demonstração** → são processadas **inteiramente no seu navegador**; nenhum dado dessas bases é enviado a servidores.

---

## O que a versão atual faz

- **Dois modelos**, na ordem de referência:
  - **INEH** — modelo completo (inclui todos os casos).
  - **IEIL** — métrica complementar, que exclui flagrantes e mortes por intervenção de agente do Estado.
- **Modelo real da tese** (DF, 2018–2023): coeficientes ajustados em Python (scikit-learn, regressão logística L2, C=0,1). Botão *"Carregar Elucidômetro oficial"* — INEH n=1342 (AUC 0,72) · IEIL n=1068 (AUC 0,71). O cálculo é feito no servidor seguro.
- **Upload de base própria (CSV)**: a ferramenta trata os dados automaticamente — reconhece/renomeia as colunas do questionário, deriva ano/mês/tempo de resposta a partir das datas, remove variáveis que vazam o resultado, normaliza o alvo (Sim/Não) e separa IEIL de INEH. O treino no navegador é uma **estimativa** (reimplementação, não idêntica ao scikit-learn).
- **Elucidômetro interativo**: ajuste as características do caso e acompanhe a probabilidade estimada em tempo real.

---

## Arquitetura

```
Frontend (GitHub Pages, público)
  ├── index.html, support.js, elucidometro_ingest.js, elucidometro_gov.js
  └── elucidometro-config.js   ← URL do servidor seguro

Servidor seguro (Cloudflare Worker, privado)
  └── contém os coeficientes do modelo; expõe POST /score → { concpc, ieil }
```

> Os coeficientes da tese ficam **apenas** no servidor (Cloudflare Worker) e **nunca** são publicados neste repositório.

---

## Créditos

- **Modelo e idealização:** Marcelo Zago — tese de doutorado no IDP (Instituto Brasileiro de Ensino, Desenvolvimento e Pesquisa).
- **Orientadores:** Felix Lopez (IPEA) e Franco Perazzoni (PF).

Ferramenta de apoio à decisão investigativa. Não mede eficácia investigativa nem deve ser usada como critério excludente.
