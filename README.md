# 🍔 Previsão de Churn: Aplicativo de Delivery ToComFome

## 📖 Contexto do Projeto
No setor de varejo e aplicativos de delivery, reter um cliente ativo é significativamente mais barato do que o Custo de Aquisição de Clientes (CAC) para trazer um novo usuário. 

O **ToComFome** é um aplicativo de entrega de comida que identificou a necessidade de entender o perfil de risco dos seus usuários. A área de CRM demandou um projeto de **Data Analytics** para classificar clientes com probabilidade de abandonar a plataforma (Churn) nos próximos meses, permitindo o direcionamento inteligente de campanhas de marketing e retenção.

Este projeto utiliza uma base de dados de 10.000 clientes para realizar uma análise exploratória profunda e treinar um modelo de Machine Learning capaz de segmentar a base pelo risco de cancelamento.

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

## 📊 Metodologia e Decisões Técnicas

**1. Definição da Variável Resposta (Target)**
* Cruzamento da tabela de clientes com a tabela de transações.
* **Regra de Negócio:** Clientes sem transações nos últimos 30 dias em relação à data de extração foram classificados como **Churn (1)**.

**2. Análise Exploratória (EDA) e Detecção de Viés**
* Utilização de **Information Value (IV)** e **Correlação Linear** para ranquear o poder preditivo de cada característica do cliente.
* ⚠️ **Decisão Crítica de Negócio (Tratamento de Overfitting):** Durante a análise, identifiquei que as variáveis `Idade` e `Qte_Categorias` apresentaram um IV suspeitamente alto (acima de 0.90). No contexto real de um aplicativo, a idade não define o cancelamento com tamanha exatidão. Para evitar o *Data Leakage* (Vazamento de Dados) e impedir que o modelo sofresse de *Overfitting* (Superajuste) focando em um viés da base didática, optei por excluir essas variáveis do treinamento.
* **Foco no que é acionável:** Após a limpeza do viés, identificamos os verdadeiros fatores de risco sólidos para o negócio, com destaque para o **Limite de Crédito no Mercado (IV: 0.46)**, seguido pelo **Score de Crédito (0.27)** e **Estado (0.17)**.

<img width="2996" height="1581" alt="grafico_iv_fatores_risco" src="https://github.com/user-attachments/assets/3e34af7d-be11-47cc-950c-ddad9fd30294" />


**3. Modelagem Preditiva e Segmentação**
* Treinamento de um algoritmo de Árvore de Decisão (`max_depth=4` para garantir interpretabilidade pelas áreas de negócio).
* O modelo otimizado gerou uma probabilidade (0% a 100%) realista para cada usuário, permitindo a criação de três segmentos de risco práticos.

---

## 💡 Resultados e Planos de Ação

Ao remover o viés estatístico da base, o modelo apresentou um funil de risco altamente focado e realista. De 10.000 usuários, mapeamos a seguinte distribuição:

| Segmento de Risco | Volumetria | % da Base |
| :--- | :--- | :--- |
| 🟢 **Baixo Risco** (< 30%) | 6.832 clientes | ~68,3% |
| 🟡 **Médio Risco** (30% a 69%) | 3.134 clientes | ~31,3% |
| 🔴 **Alto Risco** (>= 70%) | 34 clientes | ~0,3% |
<img width="2140" height="1407" alt="grafico_distribuicao_risco_otimizado" src="https://github.com/user-attachments/assets/fed58ad6-5aa5-448f-9175-90ba44582094" />


### Estratégias de CRM Propostas:
* **🔴 Para o Alto Risco (34 clientes) - Retenção VIP:** Com um funil extremamente afunilado, a equipe de CRM não precisa queimar orçamento em massa. A recomendação é uma ação *premium* (quase artesanal), como o envio de cupons agressivos (ex: R$ 50 off) associados à entrada no Programa de Fidelidade, focando em reter esses usuários críticos de forma altamente personalizada.
* **🟡 Para o Médio Risco (3.134 clientes) - Fomento de Hábito:** Este é o grande campo de batalha do app. A recomendação é implementar campanhas automatizadas de *cross-sell* via push notification e e-mail. O objetivo é incentivar compras em novas categorias para criar recorrência e fidelizar o cliente antes que ele migre para o grupo de risco iminente.
* **🟢 Para o Baixo Risco (6.832 clientes) - Manutenção de Margem:** Sendo o maior grupo da empresa, o objetivo principal é evitar a queima de margem de lucro com descontos desnecessários. O foco de investimento aqui deve ser puramente na excelência operacional (tempo de entrega ágil e suporte eficiente).

---

## 📂 Como navegar neste repositório
* A pasta principal contém o arquivo `.ipynb` com o código documentado passo a passo, detalhando toda a lógica matemática e as decisões de negócios aplicadas ao modelo.
