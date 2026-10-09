# 📊 Telecom Customer Churn Analysis & Prediction

Projeto prático desenvolvido para o curso de **Data Science da Coderhouse**, com foco em análise exploratória de dados (EDA), teste de hipóteses de negócio e modelagem preditiva de evasão de clientes (*churn*) no setor de telecomunicações.

---

## 📌 Visão Geral do Projeto

O cancelamento de serviços (*churn*) é um dos maiores desafios de retenção em empresas de telecomunicações. Este projeto investiga uma base de **7.032 clientes** contendo dados cadastrais, contratuais, financeiros, de uso de serviços e dados de experiência do cliente obtidos via Processamento de Linguagem Natural (NLP), como polaridade de sentimento e tamanho de feedback.

O pipeline abrange desde o entendimento dos dados e validação estatística de hipóteses de negócio até a seleção de variáveis e treinamento de um classificador supervisionado.

---

## 🎯 Hipóteses Analisadas & Principais Descobertas

| # | Hipótese | Validação | Conclusão |
|---|---|---|---|
| **1** | Clientes com mais tempo de casa cancelam menos. | **Confirmada** | A mediana de *tenure* (tempo em meses) entre os clientes retidos é de **38 meses**, contra apenas **10 meses** entre os que cancelaram. |
| **2** | Cobranças mensais mais elevadas aumentam o churn. | **Confirmada** | Clientes que cancelaram apresentam média de fatura de **R$ 74,44** (mediana R$ 79,65), enquanto clientes fiéis possuem média de **R$ 61,31** (mediana R$ 64,45). |
| **3** | O tipo de contrato afeta diretamente a taxa de cancelamento. | **Confirmada** | Contratos mês a mês (*month-to-month*) têm taxa de churn de **42,71%**, contra **11,28%** em contratos anuais e apenas **2,85%** em contratos bienais. |

Além disso, a análise de sentimento revelou forte correlação entre polaridades negativas de feedback textual e a decisão de cancelamento.

---

## 🛠️ Tecnologias e Bibliotecas Utilizadas

- **Linguagem:** Python
- **Manipulação de Dados:** `pandas`, `numpy`
- **Visualização de Dados:** `matplotlib`, `seaborn`
- **Machine Learning & Pré-processamento:** `scikit-learn`
  - `LabelEncoder`
  - `SelectKBest` (`f_classif`)
  - `train_test_split`
  - `DecisionTreeClassifier`
- **Consumo do Dataset:** `kagglehub`

---

## 🔬 Metodologia e Pipeline

1. **Ingestão e Limpeza dos Dados:**
   - Carga do dataset via `kagglehub` (`beatafaron/telco-customer-churn-realistic-customer-feedback`).
   - Remoção de identificadores irrelevantes (`Unnamed: 0`, `customerID`, `PromptInput`).
   - Verificação de dados faltantes (0 nulos identificados) e checagem de duplicidade.

2. **Análise Exploratória (EDA):**
   - Distribuição de classes: **73,42%** não cancelaram vs. **26,58%** cancelaram.
   - Matriz de correlação entre variáveis numéricas.
   - Gráficos de violino (sentimento vs. churn), boxplot (*tenure* vs. churn) e contagem por contrato.

3. **Engenharia de Recursos e Seleção:**
   - Codificação de variáveis categóricas via `LabelEncoder`.
   - Seleção das **Top 10 features** mais relevantes com `SelectKBest` ($k=10$, ANOVA F-test):
     - `tenure`, `OnlineSecurity`, `OnlineBackup`, `TechSupport`, `Contract`, `MonthlyCharges`, `TotalCharges`, `CustomerFeedback`, `feedback_length`, `sentiment`.

4. **Modelagem Preditiva:**
   - Divisão dos dados em treino (70%) e teste (30%) com estratificação de semente (`random_state=42`).
   - Treinamento do algoritmo **Decision Tree Classifier**.

---

## 📈 Resultados do Modelo

O modelo treinado alcançou excelente poder preditivo no conjunto de testes ($N = 2.110$ clientes):

| Métrica | Resultado |
|---|---|
| **Acurácia** | **92,61%** |
| **Precisão** | **86,68%** |
| **Recall (Sensibilidade)** | **85,13%** |
| **F1-Score** | **85,90%** |

### Matriz de Confusão

```text
               Predito: Não     Predito: Sim
Real: Não          1479              73
Real: Sim            83             475
```

- **Verdadeiros Negativos (VN):** 1.479
- **Falsos Positivos (FP):** 73
- **Falsos Negativos (FN):** 83
- **Verdadeiros Positivos (VP):** 475

---

## 💡 Insights e Ações Recomendadas para o Negócio

1. **Incentivo a Contratos Longos:** Desenvolver descontos progressivos e benefícios para migrar clientes de contratos mensais para anuais/bienais (redução potencial drástica do churn).
2. **Onboarding nos Primeiros 12 Meses:** O primeiro ano concentra o maior volume de evasão (mediana de 10 meses). Ações de boas-vindas, suporte prioritário e acompanhamento reduzem a perda inicial.
3. **Monitoramento de Satisfação Contínuo:** Utilizar o modelo de sentimento em feedbacks de atendimento para acionar gatilhos de retenção automáticos antes do pedido formal de cancelamento.

---

## 🚀 Como Executar o Projeto

### Pré-requisitos
Certifique-se de ter o Python 3.9+ instalado em sua máquina.

### Instalação

```bash
# Clone o repositório
git clone https://github.com/SEU-USUARIO/telecom-churn-analysis.git

# Acesse a pasta do projeto
cd telecom-churn-analysis

# Instale as dependências
pip install pandas numpy matplotlib seaborn scikit-learn kagglehub
```

### Execução via Jupyter ou Google Colab
Abra o arquivo `.ipynb` no seu ambiente preferido (Jupyter Lab, VS Code ou Google Colab) e execute as células sequencialmente.

---

## 👤 Autora

**Ana Luiza Mattia de Lima**  
- Estudante de Análise e Desenvolvimento de Sistemas (IFSC)  
- [LinkedIn](https://www.linkedin.com/in/ana-luiza-mattia-de-lima/)  
