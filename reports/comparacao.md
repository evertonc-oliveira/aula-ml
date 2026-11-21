# Relatório de Comparação e Decisão (`chamados-r1` vs. `chamados-r2`)

## 1. Alteração Realizada

* **Dataset:** `chamados-v1` → `chamados-v2` (branch `correcao-rotulo`, tag `dados-v2`).
* **Modificação:** Correção do rótulo do chamado de ID `006` (`"bloqueio de acesso"`) em `data/chamados.csv`, alterando a classe de `comum` para `urgente`, conforme a regra de rotulagem definida no manifesto.
* **Integridade da Partição:** O arquivo `data/split.csv` permaneceu inalterado (`split_sha256` idêntico entre `dados-v1` e `dados-v2`), garantindo avaliação justa sobre os mesmos 4 exemplos de teste.

## 2. Tabela de Métricas (Conjunto de Teste Fixo)

| Métrica / Atributo | `chamados-r1` (`dados-v1`) | `chamados-r2` (`dados-v2`) | Variação |
| :--- | :---: | :---: | :---: |
| **Acurácia Geral** | `0.75` (3/4) | `1.00` (4/4) | `+0.25` |
| **Recall (`urgente`)** | `0.50` (1/2) | `1.00` (2/2) | `+0.50` |
| **Recall (`comum`)** | `1.00` (2/2) | `1.00` (2/2) | `0.00` |
| **Suporte (`urgente` / `comum`)** | 2 / 2 | 2 / 2 | Sem alteração |

## 3. Evidências de Restauração (`modelo-r1` em Clone Limpo)

Artefatos recuperados via `git switch --detach modelo-r1` e `dvc pull` no diretório `aula-ml-restauracao` e validados contra `reports/modelo.json`:

* **Commit (`git rev-parse HEAD`):** '2ef8d64b85ee054503587b17a660109227fb0818'
* **`data/chamados.csv` (`dataset_sha256`):** 'bc3fd86a3a5f598841a58839a9726d901fa7e8361ffe79c5b43873ad8a1328ac'
* **`data/split.csv` (`split_sha256`):** '2ef820171c1a4625fe216e6da67c7c8dcf9d97a08288c0239cd23f1a6961d981'
* **`models/model.json` (`artifact_sha256`):** '72a3a67936139a3473838a6dcfa7aae1acb4c23467be1ef1056d51d485b94840'

## 4. Decisão da Revisão

**Decisão:** **ACEITAR** o modelo `chamados-r2` e mesclar a branch `correcao-rotulo` em `main`.

**Justificativa:** A correção da anotação no treino eliminou a ambiguidade do token `"bloqueio"`, elevando o recall da classe `urgente` de `0.50` para `1.00` sem degradar o recall da classe `comum` (`1.00`) na mesma partição de teste fixa.