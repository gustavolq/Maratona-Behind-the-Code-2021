# <p align='center'> **Desafio 01 - Bantonal**

## **1. Sobre a Bantonal**
A Bantonal é a plataforma bancária líder na América Latina, que resolve as operações de missão crítica das Instituições Financeiras de forma simples e precisa.

A plataforma bancária entrou no mercado em 1991 e tornou-se líder na América Latina. Sua sede se encontra no Uruguai, onde também estão localizados seu Departamento de Pesquisa e Desenvolvimento, seu Centro de Serviços de Manutenção Global e seu Centro de Treinamento. Possui escritórios comerciais e de serviços em : Argentina, Chile, Colômbia, México, Peru e Uruguai. Seus Centros de Desenvolvimento de Software estão localizados no Peru e no Uruguai.

## **2. Desafio de Negócio**

Cada vez que um cliente solicita um empréstimo a uma instituição financeira, diversos processos e controles internos são acionados, necessários para a avaliação da solicitação recebida. Dessa forma, são analisadas manualmente muitas informações relacionadas com o perfil do cliente, destinos de crédito, atividade de trabalho, rendimentos, condições de habitação, entre outros dados demográficos.

A instituição também utiliza os chamados bueraus de crédito para conhecer o histórico de crédito do cliente, a fim de definir o perfil de crédito do cliente. Em conjunto com outros registros próprios, informações de outros créditos, grau de conformidade e comportamento dos produtos contratados, a instituição aprova um valor a ser emprestado e um prazo para sua devolução ou rejeita a solicitação.

## **3. Objetivo**
O desafio consistia em criar um modelo de inteligência artificial capaz de realizar uma análise de risco para predizer se um empréstimo a um cliente deve ser feito ou não. Para isso, esperava-se a utilização de um modelo de Machine Learning capaz de realizar uma classificação.

O modelo foi treinado com os conjuntos de dados disponibilizado no repositório, contendo dados de clientes de bancos, como dados demográficos, sobre suas contas e sobre o empréstimo que querem realizar.

## **4. Tecnologias Aplicadas**
Para a construção do Modelo de Machine Learning utilizei a linguagem de programação Python, com o Jupyter Notebook.

## **5. Desenvolvimento da Solução**
O desafio consistia na elaboração de um modelo de ML para predição de risco de empréstimo, baseado em informações bancárias. No desafio também deveria ser realizado a exploração dos dados, tratamento e construção do modelo para predição.

O modelo deverá receber como entrada os seguintes dados :
```python
[
  "ID", # Número de identificação do cliente
  "CHECKING_BALANCE", # Saldo em conta corrente do cliente
  "PAYMENT_TERM", # Número de dias que o cliente tem para pagar o empréstimo
  "CREDIT_HISTORY", # Como está a situação de crédito passada do cliente
  "LOAN_PURPOSE", # Motivação do empréstimo
  "LOAN_AMOUNT", # Valor do empréstimo
  "EXISTING_SAVINGS", # Saldo de conta poupança
  "EMPLOYMENT_DURATION", # Quantos anos o cliente está no último emprego
  "INSTALLMENT_PERCENT", # Em quantas parcelas o empréstimo deve ser pago
  "SEX", # Sexo
  "OTHERS_ON_LOAN", # Se existe um fiador ou outro aplicante para o empréstimo
  "CURRENT_RESIDENCE_DURATION", # Anos em que o cliente está vivendo na última casa
  "PROPERTY", # Se o cliente possui alguma propriedade em nome
  "AGE", # Idade
  "INSTALLMENT_PLANS", # Plano de financiamento, podendo ser do banco, externo, ou nenhum
  "HOUSING", # Tem casa própria ou não
  "EXISTING_CREDITS_COUNT", # Número de empréstimos que o cliente já tem
  "JOB_TYPE", # Tipo de emprego: 0 - desempregado, 1 - Não qualificado, 2 - Autônomo, 3 - Qualificado
  "DEPENDENTS", # Número de pessoas com acesso à conta
  "TELEPHONE", # Se o cliente tem telefone cadastrado ou não
  "FOREIGN_WORKER" # Se o cliente trabalha num país externo ao do banco ou não
]
```
E como saída um valor binário que representa se o empréstimo deve ser permitido ou não (0 para não, 1 para sim).

**Atenção:** os dados disponibilizados no desafio são fictícios, qualquer correlação com a realidade é mera coincidência.

## **6. Submissão**
Para a entrega do desafio, foi realizado o preenchimento do arquivo [ANSWERS.csv](data/ANSWERS.csv) disponível no repositório, com o valor da coluna ```ALLOW``` em todas as 1000 linhas com as predições resultadas do modelo (valores 0 ou 1).

## **7. Avaliação do Modelo**
A avaliação do modelo foi realizada automaticamente utilizando os dados enviados no arquivo ```ANSWERS.csv``` para calcular uma pontuação numérica de 1 até 100, baseada na métrica **F1-Score**.

## **8. Arquivos do Repositório**
- [data](data) : Pasta com os arquivos .csv utilizados
- [Desafio01.ipynb](Desafio01.ipynb) : Arquivo do Jupyter Notebook com explorações e criação do modelo de Machine Learning.