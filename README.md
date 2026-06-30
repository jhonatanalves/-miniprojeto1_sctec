# MiniProjeto DataView — Exploração e Análise de Dados de Vendas

> Projeto avaliativo do Módulo 1 (Desenvolvedor(a) em IA para Análise Preditiva) do programa SCTEC.
> Análise exploratória de dados (EDA) de um dataset de vendas em Python, com limpeza,
> transformação, agregação, visualização e exportação de relatórios.

---

## Sobre o projeto

O **DataView** é um fluxo completo de análise exploratória de dados de vendas, desenvolvido em
um notebook Python. Ele simula o trabalho de um Analista de Dados Júnior que recebe um histórico
de vendas "sujo" e precisa entregá-lo limpo, analisado e visualizado para uma reunião de diretoria.

O notebook executa o pipeline de ponta a ponta: gera os dados brutos, inspeciona,
limpa, trata outliers, cria colunas derivadas, calcula métricas agregadas, segmenta clientes,
calcula estatísticas com NumPy, gera gráficos e exporta os resultados em CSV e JSON.

## O que o projeto analisa

- Receita total e volume de vendas por mês;
- Top 5 produtos e receita por categoria;
- Desempenho por região (receita total e ticket médio);
- Segmentação de clientes por nível de gasto (Bronze, Prata, Ouro);
- Comparação entre os dados com e sem tratamento de outliers (versões v1 e v2);
- Estatísticas gerais de receita (média, mediana, desvio padrão, percentis).

## Objetivo

Praticar os principais conceitos de Python e de análise de dados:

- Lógica de programação, variáveis, tipos de dados e operadores;
- Condicionais (`if/elif/else`) e repetição (`for`);
- Funções com parâmetros, retorno e funções `lambda`;
- Funções reutilizáveis e função de ordem superior (callback);
- Leitura e escrita de arquivos CSV e JSON;
- Módulo `datetime` para manipulação de datas;
- Expressões regulares com o módulo `re`;
- Pandas: DataFrames, limpeza, `groupby`, filtros e transformações;
- NumPy: arrays, operações vetorizadas e broadcasting;
- Detecção e tratamento de outliers (IQR);
- Matplotlib e Seaborn: gráficos, customização e exportação em PNG;
- Versionamento com Git/GitHub.

## Como executar

> **Importante sobre os caminhos:** o notebook fica em `notebooks/` e grava os arquivos em
> caminhos relativos que sobem um nível (`../data/...`, `../outputs/...`). Por isso ele precisa
> ser executado **a partir da pasta `notebooks/`**, com a raiz do projeto um nível acima.

### No Google Colab

Faça upload do arquivo dataview.ipynb e abra-o no Colab e execute todas as células.

As pastas data/ e outputs/ serão criadas automaticamente na sessão. O Colab já vem com Pandas,
NumPy, Matplotlib e Seaborn instalados.

### Localmente com VS Code

Instale o Python 3.10+ e o VS Code com a extensão Python;
Instale as dependências:


   ```bash
   pip install pandas numpy matplotlib seaborn
   ```

Abra notebooks/dataview.ipynb e execute as células na ordem. Com o BASE_DIR, os arquivos são
gravados na raiz do projeto independentemente da pasta de execução.

# Sobre os dados (v1 vs v2)

O dataset é **gerado sinteticamente** pela função `gerar_dataset_vendas()` (com `seed=42` para
reprodutibilidade), contendo problemas propositais — valores nulos, datas inválidas e espaços
extras em strings — para exercitar a limpeza. O pipeline gera duas versões processadas:

- **v1 (`data/processed/v1_com_outliers/`):** dados limpos (sem nulos, datas válidas, strings
  normalizadas), porém com os outliers **mantidos**;
- **v2 (`data/processed/v2_outliers_tratado/`):** a mesma base da v1, com os outliers **removidos**
  pelo método IQR.

**Versão escolhida para `data/final/`: v2 (outliers tratados).** A escolha se justifica porque o
objetivo final é uma base consistente para análise e futuro uso em modelos, e os valores extremos
distorceriam médias e gráficos. A v1 permanece salva para consulta e comparação.

## Estrutura do projeto

```
projeto/
├── data/
│   ├── raw/                          # Dataset bruto gerado 
│   │   └── vendas.csv
│   ├── processed/
│   │   ├── v1_com_outliers/          # Limpeza geral, outliers mantidos
│   │   │   └── vendas_v1.csv
│   │   └── v2_outliers_tratado/      # Limpeza v1 + tratamento de outliers
│   │       └── vendas_v2.csv
│   └── final/                        # Dataset escolhido (v2) para uso futuro
│       └── vendas_final.csv
├── notebooks/
│   └── dataview.ipynb                # Notebook principal de EDA (resolve a raiz via BASE_DIR)
├── outputs/
│   ├── relatorios/                   # Saídas textuais (métricas e estatísticas)
│   │   ├── metricas_por_mes.csv
│   │   ├── segmentacao_clientes.csv
│   │   └── estatisticas_gerais.json
│   └── graficos/                     # Visualizações exportadas em PNG
│       ├── receita_por_mes.png
│       ├── top_produtos.png
│       └── dist_regiao.png
└── README.md
```


## Conceitos de Python e análise de dados aplicados

| Conceito | Onde aparece no projeto |
|----------|-------------------------|
| Lógica de programação, operadores | Cálculo de receita, filtros e comparações |
| Tipos de dados (int, float, str, list, dict) | Dataset, métricas e relatório de limpeza |
| `if/elif/else` | Classificação de faixas de receita e segmentos |
| `for` | Geração do dataset e exibição de métricas |
| Funções com parâmetros e retorno | Cada etapa (limpar, transformar, agregar...) |
| Funções `lambda` (2 usos) | Segmentação de clientes (RF07) e callback (RF10) |
| Função de ordem superior (callback) | `aplicar_transformacao()` (RF10, bônus) |
| Módulo `datetime` | Extração de mês, trimestre e ano |
| Expressões regulares (`re`) | Limpeza de strings com `re.sub(r"\s+", " ", ...)` |
| Pandas — DataFrames e Series | Estrutura principal de dados |
| Pandas — filtros e seleções | Remoção de nulos, datas inválidas e outliers |
| Pandas — `groupby` | Métricas por mês, produto, categoria e região |
| NumPy — arrays e vetorização | Estatísticas sobre `receita_total` (sem loops) |
| NumPy — broadcasting | Participação percentual de cada venda |
| NumPy — `np.select` | Faixa de receita por item (condicional vetorizada) |
| Detecção/tratamento de outliers (IQR) | Geração das versões v1 e v2 |
| Matplotlib/Seaborn | Gráficos de linha, barras e boxplot |
| Exportação de gráficos (PNG) | `fig.savefig()` em `outputs/graficos/` |
| Leitura/escrita CSV | `pd.read_csv()` e `.to_csv()` |
| Leitura/escrita JSON | `json.dump()` e `json.load()` |

## Vídeo de demonstração

a ser inserido