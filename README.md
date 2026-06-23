# MiniProjeto DataView

## Sobre o projeto
O DataView é um projeto de análise exploratória de dados (EDA) de vendas,
desenvolvido em Python em um notebook. O notebook lê, limpa, transforma,
analisa e visualiza um dataset de vendas, gerando métricas e insights para
uma reunião trimestral da diretoria.

## O que o projeto analisa
- Receita total e volume de vendas por mês e trimestre
- Top produtos e categorias por receita
- Desempenho por região
- Segmentação de clientes por nível de gasto (Bronze, Prata, Ouro)
- Comparação entre os dados com e sem tratamento de outliers (v1 e v2)
- Exportação de relatórios em CSV e JSON

## Objetivo
Praticar os principais conceitos:
- Lógica de programação com Python
- Variáveis, tipos de dados e operadores
- Condicionais (if, elif, else) e repetição (for, while)
- Funções com parâmetros, retorno e funções lambda
- Funções reutilizáveis e função de ordem superior (callback)
- Leitura e escrita de arquivos CSV e JSON
- Módulo datetime para manipulação de datas
- Expressões regulares com o módulo re
- Pandas: DataFrames, limpeza, groupby, filtros e transformações
- NumPy: arrays, operações vetorizadas, broadcasting, np.select
- Detecção e tratamento de outliers (IQR)
- Matplotlib e Seaborn: gráficos, customização e exportação em PNG
- Uso básico do GitHub

## Requisitos Funcionais (RF) atendidos

| RF | Descrição | Status |
|---|---|---|
| RF01 | Criar ou Carregar o Dataset de Vendas (sintético, com dados sujos intencionais) | OK |
| RF02 | Inspecionar e Descrever os Dados (shape, dtypes, nulos, describe) | OK |
| RF03 | Limpar e Tratar os Dados (nulos, datas inválidas, strings com regex) | OK |
| RF04 | Detectar e Tratar Outliers (IQR) — gera v1 e v2 | OK |
| RF05 | Criar Colunas Derivadas (receita_total, mes, trimestre, faixa_receita_item) | OK |
| RF06 | Calcular Métricas Agregadas com groupby (mês, produto, categoria, região) | OK |
| RF07 | Segmentar Clientes por Nível de Gasto (Bronze/Prata/Ouro com lambda) | OK |
| RF08 | Calcular Estatísticas com NumPy (vetorizado, broadcasting, boolean indexing) | OK |
| RF09 | Criar Visualizações com Matplotlib e Seaborn (3 gráficos exportados em PNG) | OK |
| RF10 | Organizar o Código em Funções Reutilizáveis (docstrings, reutilização, callback) | OK |
| RF11 | Ler e Escrever Arquivos (CSV com to_csv, JSON com dump/load) | OK |
| RF12 | Consolidar a Análise e Salvar o Dataset Final (data/final/) | OK |

## Como executar

### No Google Colab (recomendado)
1. Faça upload do notebook `notebooks/dataview.ipynb`
2. Abra o arquivo carregado no Colab
3. Execute as células na ordem, de cima para baixo

### Localmente com VS Code
1. Instale o Python 3.10+ e o VS Code.
2. Instale as dependências:
   ```
   pip install pandas numpy matplotlib seaborn
   ```
3. Execute: `jupyter notebook notebooks/dataview.ipynb`

## Estrutura do projeto
```
mini-projeto_dataview/
├── .gitignore
├── README.md
├── data/
│   ├── raw/
│   │   └── vendas.csv                  # Dataset bruto gerado (RF01)
│   ├── processed/
│   │   ├── v1_com_outliers/
│   │   │   └── vendas_v1.csv           # Limpeza geral, outliers mantidos (RF03)
│   │   └── v2_outliers_tratado/
│   │       └── vendas_v2.csv           # v1 + tratamento de outliers IQR (RF04)
│   └── final/
│       └── vendas_final.csv            # Dataset final com colunas derivadas (RF12)
├── notebooks/
│   └── dataview.ipynb                  # Notebook principal — classe DataViewPipeline (RF01-RF12)
├── outputs/
│   ├── metricas_por_mes.csv            # Métricas agregadas por mês (RF11)
│   ├── segmentacao_clientes.csv        # Segmentação Bronze/Prata/Ouro (RF11)
│   ├── estatisticas_gerais.json        # Estatísticas NumPy (RF11)
│   └── graficos/
│       ├── receita_por_mes.png         # Gráfico de linha — tendência mensal (RF09)
│       ├── top_produtos.png            # Gráfico de barras — top 5 produtos (RF09)
│       ├── dist_regiao.png             # Boxplot — distribuição por região (RF09)
│       ├── stripplot_antes.png         # Stripplot antes da remoção de outliers (RF04)
│       ├── stripplot_depois.png        # Stripplot depois da remoção de outliers (RF04)
│       ├── stripplot_com_outliers.png  # Stripplot v1 com outliers (RF04)
│       └── stripplot_sem_outliers.png  # Stripplot v2 sem outliers (RF04)
```

## Decisão sobre v1 vs v2
A base escolhida para `data/final/vendas_final.csv` foi a **v2 (outliers
tratados pelo método IQR)**, por refletir melhor o comportamento típico de
vendas para a análise da diretoria. A v1 (com outliers mantidos) permanece
disponível em `data/processed/v1_com_outliers/` para consulta futura.

**Justificativa da escolha v2:**
- Valores extremos de `quantidade` (acima de 6 unidades) e `receita_total`
  (acima de R$ 704,65) foram removidos pois distorcem médias e
  agregações, comprometendo a tomada de decisão baseada em dados.
- O método IQR (fator 1.5) é robusto e não depende de distribuição normal,
  sendo adequado para dados de vendas reais.
- A v2 preserva a grande maioria dos registros (12.579 de 13.406 — 93,8%),
  garantindo representatividade estatística.

## Ferramentas utilizadas
- Python 3.10+
- Google Colab / VS Code
- Bibliotecas: pandas, numpy, matplotlib, seaborn, re, datetime, os, random, json
- GitHub para versionamento

## Vídeo de demonstração
[Inserir link do Google Drive ou YouTube aqui]