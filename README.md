# Versionamento de Dados e Modelos (`aula-ml`)

Repositório da Atividade Prática 07 de Engenharia de Sistemas Inteligentes (UFC – CK0444), demonstrando o versionamento reprodutível de datasets, partições e modelos de classificação de chamados com **Git** e **DVC**.

## Pré-requisitos

* **Git**
* **Python 3.10** ou superior (utiliza apenas a biblioteca padrão)
* **DVC 3** (`pip install dvc` ou `pipx install 'dvc>=3,<4'`)

## Configuração do Armazenamento DVC

Os dados (`data/*.csv`) e os modelos treinados (`models/model.json`) são armazenados fora do Git, em um diretório remoto local chamado `dvc-storage`, posicionado ao lado da pasta deste repositório (`../dvc-storage`):

```bash
mkdir -p ../dvc-storage
dvc remote add -d storage ../dvc-storage
```

## Restauração de Versões Anteriores

Para recuperar o código, os dados e o artefato exato de uma versão registrada (por exemplo, `modelo-r1` ou `modelo-r2`) sem precisar executar um novo treinamento:

1. Clone o repositório e entre na pasta:
   ```bash
   git clone https://github.com/evertonc-oliveira/aula-ml.git
   cd aula-ml
   ```

2. Aponte para a tag desejada (`modelo-r1` ou `modelo-r2`):
   ```bash
   git switch --detach modelo-r1
   ```

3. Baixe os dados e o modelo correspondentes a partir do armazenamento DVC (garantindo que o caminho configurado em `dvc remote list` aponte para o diretório `dvc-storage`):
   ```bash
   dvc pull
   ```