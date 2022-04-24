# <p align='center'> **Desafio 05 - SONDA**

  - [**1. Sobre a SONDA**](#1-sobre-a-sonda)
  - [**2. Desafio de Negócio**](#2-desafio-de-negócio)
  - [**3. Objetivo**](#3-objetivo)
  - [**4. Tecnologias Utilizadas**](#4-tecnologias-utilizadas)
  - [**5. Desenvolvimento da Solução**](#5-desenvolvimento-da-solução)
  - [**6. Sobre a Avaliação**](#6-sobre-a-avaliação)

## **1. Sobre a SONDA**
A SONDA é a principal rede latino-americana de serviços de Tecnologia da Informação (TI). Em seus quase 45 anos de história na região, caracterizou-se por contar com uma oferta integral de serviços e soluções de TI, uma visão de aliado tecnológico para abordar projetos e uma sólida posição financeira, prestando de forma consistente serviços e soluções alinhadas com as estratégias de negócio de seus clientes.

Desde 1974, a missão da empresa tem sido agregar valor às atividades e negócios de seus clientes e impulsionar seu crescimento através de uma melhor utilização das tecnologias da informação, construindo relações de longo prazo que se traduzem em uma proximidade com seu trabalho e evolução.

## **2. Desafio de Negócio**
O desafio consistiu em um problema comum na área de Ciência de Dados. Um cliente expõe um problema específico de sua área e através da sua análise encontrar uma possível solução. Um cliente da área de telecomunicações reportou problema de perda de clientes (*churn*) e gostaria de conseguir identificar essa possível perda antes que ela ocorra, poor meio de Inteligência Artificial.

## **3. Objetivo**
O desafio consistiu em implementar um algoritmo de Machine Learning para classificação binária, capaz de identificar se um cliente será perdido ou não.

## **4. Tecnologias Utilizadas**
Para este desafio, utilizei a linguagem Python com o Jupyter Notebook.

## **5. Desenvolvimento da Solução**
O desenvolvimento consistiu no uso de um algoritmo de Machine Learning de Aprendizagem Supervionada, como o de [Árvore de Decisão](https://scikit-learn.org/stable/modules/tree.html), para realizar uma classificação binária que dirá se um cliente será perdido ou não.

As classificações devem ser salvas no arquivo de respostas [ANSWERS.csv](data/ANSWERS.csv), da mesma forma aparecem no dataset (``Yes`` ou ``No``). Todos os clientes precisam ter uma classificação.

O dicionário de dados é o seguinte:

| Coluna           | Descrição                                                                                                          |
| ---------------- | ------------------------------------------------------------------------------------------------------------------ |
| ID               | Customer ID                                                                                                        |
| GENDER           | Whether the customer is a male or a female                                                                         |
| SENIORCITIZEN    | Whether the customer is a senior citizen or not (1, 0)                                                             |
| PARTNER          | Whether the customer has a partner or not (Yes, No)                                                                |
| DEPENDENTS       | Whether the customer has dependents or not (Yes, No)                                                               |
| TENURE           | Number of months the customer has stayed with the company                                                          |
| PHONESERVICE     | Whether the customer has a phone service or not (Yes, No)                                                          |
| MULTIPLELINES    | Whether the customer has multiple lines or not (Yes, No, No phone service)                                         |
| INTERNETSERVICE  | Customer’s internet service provider (DSL, Fiber optic, No)                                                        |
| ONLINESECURITY   | Whether the customer has online security or not (Yes, No, No internet service)                                     |
| ONLINEBACKUP     | Whether the customer has online backup or not (Yes, No, No internet service)                                       |
| DEVICEPROTECTION | Whether the customer has device protection or not (Yes, No, No internet service)                                   |
| TECHSUPPORT      | Whether the customer has tech support or not (Yes, No, No internet service)                                        |
| STREAMINGTV      | Whether the customer has streaming TV or not (Yes, No, No internet service)                                        |
| STREAMINGMOVIES  | Whether the customer has streaming movies or not (Yes, No, No internet service)                                    |
| CONTRACT         | The contract term of the customer (Month-to-month, One year, Two year)                                             |
| PAPERLESSBILLING | Whether the customer has paperless billing or not (Yes, No)                                                        |
| PAYMENTMETHOD    | The customer’s payment method (Electronic check, Mailed check, Bank transfer (automatic), Credit card (automatic)) |
| MONTHLYCHARGES   | The amount charged to the customer monthly                                                                         |
| TOTALCHARGES     | The total amount charged to the customer                                                                           |
| CHURN            | Whether the customer churned or not (Yes or No)                                                                    |

## **6. Sobre a Avaliação**
A avaliação foi realizada de forma automática e utilizou os dados enviados para calcular uma pontuação numérica de 1 até 100, baseada na métrica [F<sub>1</sub>](https://en.wikipedia.org/wiki/F-score).