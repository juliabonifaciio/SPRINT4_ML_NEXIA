<div align="center">

```
███╗   ██╗███████╗██╗  ██╗██╗ █████╗
████╗  ██║██╔════╝╚██╗██╔╝██║██╔══██╗
██╔██╗ ██║█████╗   ╚███╔╝ ██║███████║
██║╚██╗██║██╔══╝   ██╔██╗ ██║██╔══██║
██║ ╚████║███████╗██╔╝ ██╗██║██║  ██║
╚═╝  ╚═══╝╚══════╝╚═╝  ╚═╝╚═╝╚═╝  ╚═╝
```

# SPRINT 4 — Produto de Dados com Explicabilidade

**Previsao de Visitacao em Parques Nacionais**

[![Python](https://img.shields.io/badge/Python-3.11-00C9A7?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![XGBoost](https://img.shields.io/badge/XGBoost-Tuned-FFB400?style=for-the-badge&logo=xgboost&logoColor=white)](https://xgboost.readthedocs.io)
[![SHAP](https://img.shields.io/badge/SHAP-Explainability-FF6B6B?style=for-the-badge)](https://shap.readthedocs.io)
[![Streamlit](https://img.shields.io/badge/Streamlit-App-4ECDC4?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-A78BFA?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)

</div>

-----

## Sobre o Projeto

Pipeline completa de Machine Learning aplicada ao problema de **previsao de visitacao em parques nacionais brasileiros**. O produto de dados entrega previsoes interpretaveis com suporte a decisao operacional, simulando um totem de atendimento ao turista com explicacoes em linguagem natural via SHAP.

> “Nao basta prever — e preciso explicar e gerar valor.”

-----

## Equipe — Nexia

|Nome                            |RM      |
|--------------------------------|--------|
|Alexandre Silva Alves           |RM567415|
|Julia Marcela de Faria Bonifacio|RM566673|
|Mariana Pergentino Fonseca      |RM568252|
|Pedro Iavarone Custodio         |RM567638|

-----

## Estrutura do Notebook

```
SPRINT4_ML_NEXIA.ipynb
│
├── Secao 1 — Instalacao e Configuracao
│     Dependencias e imports
│
├── Secao 2 — Geracao e Carga de Dados
│     Dataset sintetico realista de visitacao
│     5 parques × 3 anos × variaveis climaticas
│
├── Secao 3 — Analise Exploratoria (EDA)
│     Series temporais, padroes semanais/mensais
│     Impacto da precipitacao, mapa de correlacoes
│
├── Secao 4 — Engenharia de Features
│     21 variaveis: ciclicas, flags, interacoes
│     Indice de atratividade sintetico
│
├── Secao 5 — Modelagem: Regressao
│     Random Forest (baseline)
│     XGBoost + Optuna (50 trials de tuning)
│
├── Secao 6 — Modelagem: Classificacao
│     Alta / Media / Baixa demanda
│     Matriz de confusao
│
├── Secao 7 — Explicabilidade SHAP
│     Summary plot global
│     Beeswarm plot
│     Explicacao local com linguagem natural
│
├── Secao 8 — Produto de Dados (Totem)
│     Interface de decisao interativa
│     3 cenarios simulados
│
├── Secao 9 — Avaliacao Critica
│     Limitacoes, melhorias e riscos
│
└── Secao 10 — Codigo Streamlit
      app.py completo para deploy
```

-----

## Modelos e Metricas

|Modelo                  |MAE|RMSE|R²    |
|------------------------|---|----|------|
|Random Forest (baseline)|—  |—   |> 0.90|
|XGBoost + Optuna        |—  |—   |> 0.92|


> Metricas exatas sao geradas na execucao do notebook (variam por seed).

-----

## Funcionalidades do Produto

### Entrada

- Data da previsao
- Parque nacional
- Temperatura (°C)
- Precipitacao (mm)
- Flag de feriado

### Saida

- Numero previsto de visitantes
- Nivel de demanda: **Alta / Media / Baixa**
- Probabilidades por classe
- Explicacao SHAP em linguagem natural
- Recomendacao operacional automatica

### Exemplo de saida

```
Previsao: 1.842 visitantes
Nivel:    ALTA DEMANDA

Por que essa previsao?
  + atratividade:  +320 visitantes
  + eh_feriado:    +210 visitantes
  + eh_fds:        +180 visitantes
  - precipitacao:   -15 visitantes

Recomendacao: Ativar equipes extras, abrir filas
alternativas e monitorar capacidade em tempo real.
```

-----

## Como Executar

### Google Colab (recomendado)

```
1. Abra o arquivo SPRINT4_ML_NEXIA.ipynb no Google Colab
2. Execute a Secao 1 para instalar as dependencias
3. Execute todas as celulas em ordem
```

### Localmente

```bash
# Instalar dependencias
pip install shap xgboost lightgbm optuna plotly kaleido streamlit

# Abrir notebook
jupyter notebook SPRINT4_ML_NEXIA.ipynb

# Rodar app Streamlit (Secao 10)
streamlit run app_streamlit.py
```

-----

## Tecnologias Utilizadas

|Categoria       |Bibliotecas                    |
|----------------|-------------------------------|
|Machine Learning|scikit-learn, XGBoost, LightGBM|
|Explicabilidade |SHAP (TreeExplainer)           |
|Otimizacao      |Optuna                         |
|Visualizacao    |Matplotlib, Seaborn, Plotly    |
|Produto         |Streamlit                      |
|Base            |Python 3.11, pandas, NumPy     |

-----

## Limitacoes e Riscos

- **Dados sinteticos** — metricas podem ser otimistas em relacao a dados reais
- **Sem series temporais** — modelos ARIMA/Prophet capturariam melhor autocorrelacao
- **Eventos atipicos** — pandemias e catastrofes nao estao modelados
- **Deriva de conceito** — padroes de turismo mudam ao longo do tempo
- **Overfitting potencial** — validacao temporal seria mais robusta que split aleatorio

-----

## Conexao com o Negocio

```
Previsao do modelo  →  Decisao operacional  →  Impacto medido
──────────────────────────────────────────────────────────────
Alta demanda        →  Alocar +50% de staff  →  Fila -30min
Baixa demanda       →  Reduzir turnos        →  Custo -20%
Chuva prevista      →  Alertar turistas      →  Satisfacao +15%
Feriado detectado   →  Reforcar seguranca    →  Incidentes -40%
```

-----

<div align="center">

**FIAP — Machine Learning & Cognitive Computing**
**Sprint 4 · 2026 · Grupo Nexia**

</div>