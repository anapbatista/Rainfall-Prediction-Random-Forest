# Previsão de Chuva em São Carlos com Random Forest, XGBoost e MLP

---

# Objetivo

Prever se houve chuva em São Carlos utilizando dados meteorológicos históricos do Instituto Nacional de Meteorologia.

O problema foi tratado como:

* Aprendizado Supervisionado
* Classificação Binária

---

# Dataset

Fonte oficial:

[INMET - Dados Históricos](https://portal.inmet.gov.br/dadoshistoricos?utm_source=chatgpt.com)

## Dados utilizados

* Período: 2006–2025
* Dados horários da estação de São Carlos
* Dataset final diário com 7210 registros

## Tratamento realizado

* Padronização dos arquivos
* Remoção de valores inválidos
* Interpolação de dados faltantes
* Agregação horária → diária

---

# Modelo

Foram implementados e comparados quatro modelos de classificação para prever a ocorrência de chuva, visando encontrar o melhor equilíbrio entre acurácia e sensibilidade (Recall):

1. **Random Forest Classifier**: Utilizado com `class_weight='balanced'` e `n_estimators=100`. Escolhido por sua robustez a ruídos e capacidade de ranquear a importância das variáveis.
2. **XGBoost**: Configurado com `scale_pos_weight` para tratar o desbalanceamento dos dados.
3. **MLP (Rede Neural)**: Uma rede neural de múltiplas camadas para capturar padrões complexos não-lineares.
4. **Regressão Logística Polinomial (Grau 2)**: Utilizada para capturar as interações entre variáveis climáticas que um modelo puramente linear ignoraria.

---

# Resultados

## Comparativo de Performance

| Modelo | Acurácia | Recall (Chuva) | F1-Score |
| :--- | :---: | :---: | :---: |
| Random Forest | 0.84 | 0.73 | 0.76 |
| XGBoost | 0.84 | 0.84 | 0.79 |
| MLP (Neural Net) | 0.84 | 0.78 | 0.77 |
| **Logística Polinomial** | **0.84** | **0.86** | **0.79** |

## Conclusões dos Resultados

* **Recall Superior**: O modelo de **Regressão Logística Polinomial** apresentou a melhor sensibilidade (**0.86**), sendo o mais eficaz em identificar corretamente os dias de chuva.
* **Estabilidade**: A validação cruzada confirmou que o modelo polinomial é estável, com acurácia média de **0.839**.
* **Poder de Discriminação**: A curva ROC-AUC do modelo polinomial atingiu **0.924**, superando os demais modelos e demonstrando excelente capacidade de separação entre as classes.

---

## Variáveis mais importantes

* Umidade relativa
* Ponto de orvalho
* Radiação global
* Pressão atmosférica
* Temperatura do ar

---

# Tecnologias

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Seaborn

---

# Como Executar

Instale as dependências:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn requests
```

Abra o notebook:

```bash
jupyter notebook
```

---

# Estrutura do Projeto

```text
.
├── Rainfall_Predicition_Sao_Carlos.ipynb
├── data/
        ├── sao_carlos_part_1.csv
        ├── sao_carlos_part_2.csv
        ├── sao_carlos_part_3.csv
        ├── sao_carlos_part_4.csv
└── README.md
```

---

# Disciplina

SCC0230 — Inteligência Artificial
SCC0276 - Aprendizado de Máquina

Universidade de São Paulo — Instituto de Ciências Matemáticas e de Computação
