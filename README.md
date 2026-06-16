# 🍔 Previsão de Churn: Aplicativo de Delivery ToComFome

## 📖 Contexto do Projeto
No setor de varejo e aplicativos de delivery, reter um cliente ativo é significativamente mais barato do que o Custo de Aquisição de Clientes (CAC) para trazer um novo usuário. 

O **ToComFome** é um aplicativo de entrega de comida que identificou a necessidade de entender o perfil de risco dos seus usuários. A área de CRM demandou um projeto de **Data Analytics** para classificar clientes com probabilidade de abandonar a plataforma (Churn) nos próximos meses, permitindo o direcionamento inteligente de campanhas de marketing e retenção.

Este projeto utiliza uma base de dados de 10.000 clientes (fornecida pela Preditiva Analytics) para realizar uma análise exploratória profunda e treinar um modelo de Machine Learning capaz de segmentar a base pelo risco de cancelamento.

---

## 🎯 Objetivos de Negócio
Responder a três perguntas fundamentais da diretoria:
1. Quais fatores de risco estão associados com o Churn de clientes?
2. Como segmentar os clientes com a probabilidade de darem Churn nos próximos 4 meses?
3. Quais os possíveis planos de ação que a empresa pode adotar para diminuir a perda de receita?

---

## 🛠️ Tecnologias e Ferramentas Utilizadas
Todo o pipeline de dados, desde a preparação até a modelagem preditiva, foi desenvolvido em **Python** utilizando o Google Colab.
* **Manipulação e Limpeza:** `pandas`, `numpy`
* **Análise Estatística:** `scorecardpy` (Cálculo de Information Value - IV)
* **Machine Learning:** `scikit-learn` (Decision Tree Classifier)

---

## 📊 Metodologia

**1. Definição da Variável Resposta (Target)**
* Cruzamento da tabela de clientes com a tabela de transações.
* **Regra de Negócio:** Clientes sem transações nos últimos 30 dias em relação à data de extração foram classificados como **Churn (1)**.

**2. Análise Exploratória (EDA)**
* Utilização de **Information Value (IV)** e **Correlação Linear** para ranquear o poder preditivo de cada característica do cliente.
* **Principais Descobertas:** A idade e o limite de crédito possuem forte impacto no abandono. Por outro lado, a participação no **Programa de Fidelidade** atua como o principal fator de proteção contra o Churn.

**3. Modelagem Preditiva e Segmentação**
* Treinamento de um algoritmo de Árvore de Decisão (`max_depth=4` para garantir interpretabilidade pelas áreas de negócio).
* O modelo gerou uma probabilidade (0% a 100%) para cada usuário, permitindo a criação de três segmentos de risco.

---

## 💡 Resultados e Planos de Ação

De uma base de 10.000 usuários, o modelo mapeou a seguinte distribuição de risco:

| Segmento de Risco | Volumetria | % da Base |
| :--- | :--- | :--- |
| 🟢 **Baixo Risco** (< 30%) | 7.997 clientes | ~80% |
| 🟡 **Médio Risco** (30% a 69%) | 1.424 clientes | ~14,2% |
| 🔴 **Alto Risco** (>= 70%) | 579 clientes | ~5,8% |

### Estratégias de CRM Propostas:
* **Para o Alto Risco (579 clientes):** Focar o orçamento de retenção exclusivamente neste grupo. Como possuem perfil de maior poder aquisitivo (alto limite de crédito), a sugestão é rodar uma campanha VIP oferecendo adesão gratuita ao Programa de Fidelidade (nosso maior protetor de churn) atrelada a um cupom de alto valor em restaurantes premium.
* **Para o Médio Risco (1.424 clientes):** Fomentar a criação de novos hábitos. Campanhas de *cross-sell* via push notification incentivando compras em categorias diferentes das habituais (ex: se só compra hambúrguer, oferecer cupom para farmácia ou pizza).
* **Para o Baixo Risco (7.997 clientes):** Manutenção da margem de lucro. Evitar o envio de descontos agressivos, focando apenas na excelência da experiência de entrega.

---

## 📂 Como navegar neste repositório
* A pasta principal contém o arquivo `.ipynb` com o código documentado passo a passo, detalhando toda a lógica matemática e de negócios aplicada.
