# <p align='center'> **Desafio 03 - GFT**

- [<p align='center'> **Desafio 03 - GFT**](#p-aligncenter-desafio-03---gft)
  - [**1. Sobre a GFT**](#1-sobre-a-gft)
  - [**2. Desafio de Negócio**](#2-desafio-de-negócio)
  - [**3. Tecnologias Aplicadas**](#3-tecnologias-aplicadas)
  - [**4. Desenvolvimento da Solução**](#4-desenvolvimento-da-solução)
  - [**5. Submissão**](#5-submissão)
  - [**6. Avaliação do Modelo**](#6-avaliação-do-modelo)

## **1. Sobre a GFT**

A GFT é uma empresa especializada em serviços de tecnologia para o segmento financeiro, com foco em apoiar as jornadas de transformação digital dos clientes, entregando inovação, qualidade, tecnologia de ponta com agilidade e escala.

Possui vasta experiência atendendo o setor financeiro, desde banco de varejo a mercados de capitais. Além disso, também está impulsionando a transformação digital dos setores de seguros e indústria.

A GFT tem 34 anos de inovação, desde 1987 moldando o progresso tecnológico no mundo. Está presente em 15países, com mais de 7.000 colaboradores no mundo, e só no Brasil tem mais de 2.500. A GFT acredita em um mundo digital, e que para um crescimento exponencial é preciso ser inovador na área de TI.

Com a GFT, a tecnologia oferece um claro valor de negócios, capacitando os clientes a serem líderes nos seus mercados.

## **2. Desafio de Negócio**
O desafio GFT de *Open Finance* permitiu aos participantes do evento deparar-se coma nova realidade de compartilhamento de informações, confrontando bases de três instituições diferentes, dois bancos e uma seguradora e a partir destes dados, desenvolver uma visão holística aprimorada do cliente e via Ciência de Dados, realizar a modelagem da melhor oferta e cesta de produtos para estes clientes.

A *Open Finance* é a evolução do *Open Banking* e é o sistema financeiro aberto que vai trazer mais transparência e autonomia para os usuários. Com ele, será possível que um indivíduo decida quais instituições terão acesso às suas informações, para quais finalidades e período específicos. Conforme a evolução da implementação do Open Finance, haverá a possibilidade de compartilhamento de dados sobre seguros, investimentos, fundos de pensão e previdência. 

A implementação do Open Finance no Brasil foi dividida em quatro fases. São elas:

**1. Abertura de dados das instituições**
   - A primeira fase, que teve início em fevereiro/21, foi quando as instituições financeiras disponibilizaram ao público informações básicas, como canais de atendimento e serviços oferecidos.

**2. Compartilhamento de dados dos clientes**
   - Clientes passam a ter papel ativo no compartilhamento de suas informações, podendo, se assim desejarem, dividir dados que fazem a diferença para uma oferta de produtos melhores (dados cadastrais, de transações de conta, de cartão e os dados das operações de crédito).

**3. Iniciação de pagamento e encaminhamento de proposta de operação de crédito**
   - Nessa fase, começa a integração de serviços com as transações de pagamento e encaminhamento de propostas de operações de crédito acontecendo em um ambiente unificado.

**4. Outros dados de produtos e serviços**
   - Esta fase será responsável pela inclusão de serviços mais complexos (como investimentos, previdência, seguros e câmbio) no sistema.

Em uma visão de open Finance o Banco de Varejo (RetailBankEFG) tem acesso via open finance, com o devido consentimento dos clientes, as informações da instituição financeira (InvestmentBankCDE) um banco de investimentos e as informações destes clientes referente a outra instituição financeira uma seguradora (InsuranceCompanyABC).

## **3. Tecnologias Aplicadas**
Para a construção do Modelo de Machine Learning utilizei a linguagem de programação Python, com o Jupyter Notebook.

## **4. Desenvolvimento da Solução**
Os conjuntos de dados [InvestmentBankCDE](data/InvestmentBankCDE.csv) e [RetailBankEFG](data/RetailBankEFG.csv) contém dados de compras passadas dos clientes, assim como o conjunto [InsuranceCompanyABC](data/InsuranceCompanyABC.csv), que inclui também alguns dados demográficos de seus clientes.

O desafio consistia na utilização de um algoritmo de Machine Learning de aprendizagem não-supervisionada, como os de [Regra de Associação](https://en.wikipedia.org/wiki/Association_rule_learning#Algorithms), para criar recomendações de produtos aos clientes da base de dados. Os dados dos clientes coletados das três instituições devem ser usados, e até três recomendações de produtos podem ser feitas. Para as recomendações, foi considerada uma **confiança de regra de 80%** e um **suporte mínimo de 10%**, com um **máximo de 5 antecedentes**.

A tarefa dos participantes foi realizar a análise dos dados e criar um modelo para recomendações a partir desses dados. As recomendações (até 3 por cliente) foram salvas no arquivo [ANSWERS.csv](data/ANSWERS.csv).

Os nomes de produtos nas recomendações deveriam aparecer da exata forma como estavam nas colunas dos conjuntos de dados, sendo os seguintes :

```py
[
  "seguro auto",
  "seguro vida Emp",
  "seguro vida PF",
  "Seguro Residencial",
  "Investimento Fundos_cambiais",
  "Investimento Fundos_commodities",
  "Investimento LCI",
  "Investimento LCA",
  "Investimento Poupanca",
  "Investimento Fundos Multimercado",
  "Investimento Tesouro Direto",
  "Financiamento Casa",
  "Financiamento Carro",
  "Emprestimo _pessoal",
  "Emprestimo _consignado",
  "Emprestimo _limite_especial",
  "Emprestimo _educacao",
  "Emprestimo _viagem",
  "Investimento CDB",
  "Investimento Fundos"
]
```

## **5. Submissão**
Para realizar a entrega do desafio, foi realizada as alterações no arquivo [ANSWERS.csv](data/ANSWERS.csv) disponível no repositório, preenchendo o valor das colunas de recomendação e confiança.

## **6. Avaliação do Modelo**
A avaliação do modelo foi realizada automaticamente utilizando os dados enviados no arquivo [ANSWERS.csv](data/ANSWERS.csv) para calcular uma pontuação numérica de 1 até 100, com base no nível de assertividade das recomendações, juntamente com o nível de confiança nas mesmas.