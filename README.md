# Aplicação de Machine Learning e Modelos de Preços Hedônicos na Precificação de Imóveis Residenciais em São Paulo

**Autor:** Gabriel Silva Medina

Este repositório contém o código, dados e documentação do Trabalho de Conclusão de Curso (TCC) apresentado ao curso de Ciência da Computação. O projeto foca no desenvolvimento de um sistema robusto de precificação imobiliária para a cidade de São Paulo, utilizando técnicas avançadas de Machine Learning e dados reais de transações (ITBI).

---

## 📄 Resumo do Projeto

O mercado imobiliário é marcado por assimetria de informações e subjetividade na formação de preços. Este trabalho propõe uma abordagem baseada em dados (**Data-Driven**) para mitigar esse problema, utilizando modelos de preços hedônicos.

Diferente de avaliações baseadas em preços de anúncios (que contêm viés de oferta), este estudo utiliza **dados oficiais de transações (ITBI)** da Prefeitura de São Paulo, abrangendo o período de **2006 a 2024**.

A metodologia seguiu um fluxo inspirado no **CRISP-DM**, culminando na criação de modelos preditivos segregados por tipo de imóvel (Vertical e Horizontal) que superaram significativamente os métodos tradicionais de avaliação.

### Principais Resultados
| Segmento | Melhor Modelo | RMSE (Erro Médio) | R² (Explicação) | Melhoria vs Baseline |
| :--- | :--- | :--- | :--- | :--- |
| **Vertical (Apartamentos)** | **H2O Stacked Ensemble** | R$ 184.424,82 | **0.7521** | **-17.6%** erro |
| **Horizontal (Casas)** | **H2O GBM** | R$ 302.382,49 | **0.5618** | **-11.0%** erro |

> **Conclusão:** A utilização de algoritmos não-lineares e a segmentação de mercado provaram ser estratégias essenciais, com os modelos de AutoML superando largamente as regressões lineares clássicas.

---

## 🚀 Metodologia e Pipeline

O desenvolvimento foi documentado detalhadamente no Jupyter Notebook `TCC_v5.ipynb`, estruturado nas seguintes etapas:

### 1. Coleta e Validação (Etapa 1)
- Validação estrutural de 19 anos de arquivos `.xlsx` (2006-2024).
- Garantia de consistência de colunas e abas mensais em mais de **2.3 milhões de registros**.

### 2. Engenharia de Dados e Features (Etapas 2 e 3)
- **Enriquecimento Geográfico:** Cruzamento de CEPs para obtenção de Latitude, Longitude e Bairro.
- **Ajuste Monetário:** Correção de todos os valores históricos de transação para valores presentes (2024) utilizando o **IPCA** acumulado.
- **Clusterização Geoespacial (K-Means):** Criação de uma *feature* de "Zona" (Cluster 0-7) para capturar a valorização regional além da coordenada exata.

### 3. Análise Exploratória e Segmentação (AED)
- Identificação de dinâmicas de preço distintas entre imóveis verticais e horizontais.
- **Decisão Estratégica:** Segregação dos datasets para treinamento de modelos especialistas.

### 4. Modelagem e Avaliação (Etapas 7 a 13)
- **Baseline:** Regressão Linear, Ridge e Árvore de Decisão.
- **Divisão Temporal Estrita:**
    - *Treino:* 2006-2015
    - *Validação:* 2016-2020
    - *Teste:* 2021-2024 (isolado para avaliação final)
- **AutoML (H2O.ai):** Utilização de validação cruzada (5-fold) para treinar e otimizar automaticamente modelos complexos (GBM, Random Forest, Deep Learning, Stacked Ensembles).

---

## 🛠️ Tecnologias Utilizadas

*   **Linguagem:** Python 3.10+
*   **Análise de Dados:** Pandas, NumPy
*   **Visualização:** Matplotlib, Seaborn
*   **Machine Learning Clássico:** Scikit-learn
*   **AutoML & Modelagem Avançada:** **H2O.ai** (Java based)
*   **Ambiente:** Google Colab / Jupyter Notebook

---

## 📂 Estrutura do Repositório

```
.
├── TCC_v5.ipynb              # Notebook principal com todo o código (Pipeline completa)
├── APLICAÇÃO.../             # Arquivos LaTeX do texto do TCC
│   ├── capitulos/            # Capítulos teóricos (Introdução, Metodologia, Resultados...)
│   └── main.pdf              # Versão compilada do trabalho escrito
├── annotated-tcc...pdf       # PDF do TCC com anotações
├── README.md                 # Documentação do projeto
└── ...
```

---

## 💻 Como Executar o Projeto

O código foi originalmente desenvolvido para o ambiente **Google Colab**, montando o Google Drive para leitura dos dados. Para executar localmente, siga os passos abaixo:

### Pré-requisitos
- Python 3.8+
- Java (necessário para o H2O)
- Pip (gerenciador de pacotes)

### 1. Instalação

Clone o repositório e instale as dependências:

```bash
git clone https://github.com/GabrielSMedina/TCC_modelo_hedonico.git
cd TCC_modelo_hedonico

# Recomenda-se usar um ambiente virtual
python -m venv venv
source venv/bin/activate  # Linux/Mac
# ou .\venv\Scripts\activate no Windows

pip install pandas numpy matplotlib seaborn scikit-learn h2o notebook
```

### 2. Configuração dos Dados

O notebook espera uma estrutura de diretórios específica. Localmente, você precisará:

1.  Baixar os dados públicos do ITBI (Prefeitura de SP) ou usar seus processados.
2.  Ajustar a variável `DRIVE_BASE_PATH` no início do notebook `TCC_v5.ipynb`:

```python
# No Colab era:
# DRIVE_BASE_PATH = '/content/drive/MyDrive/dados_tcc'

# Para local, mude para:
DRIVE_BASE_PATH = './dados'  # Crie uma pasta 'dados' na raiz e coloque os arquivos lá
```

### 3. Execução

Inicie o Jupyter Notebook:

```bash
jupyter notebook
```

Abra o arquivo `TCC_v5.ipynb` e execute as células.

> **Aviso:** A etapa de AutoML com H2O pode ser intensiva em memória RAM. Se estiver rodando localmente, certifique-se de ter memória disponível ou reduza o parâmetro `max_runtime_secs` nas funções de treinamento.

---

## 📜 Licença e Citação

Este projeto foi desenvolvido como parte dos requisitos para obtenção do grau de Bacharel em Ciência da Computação.

**Citação do Trabalho:**
> MEDINA, Gabriel S. *Aplicação de Machine Learning e Modelos de Preços Hedônicos na Precificação de Imóveis Residenciais em São Paulo*. 2025. TCC (Bacharelado em Ciência da Computação) - Centro Universitário Serra dos Órgãos, Teresópolis, 2025.
