# <p align='center'> **Desafio 02 - Quanam**

## **1. Sobre Quanam e Aleph**
*Quanam* é uma federação internacional de empresas cujo objetivo é a inovação e a gestão do conhecimento para o benefício dos clientes e da comunidade através da consultoria empresarial, gestão e aplicação de tecnologias de pontas em diferentes segmentos.

A Quanam mantém diversas atividades a nível internacional, possui 7 escritórios na América, mais de 600 clientes e 400 especialistas altamente especializados.

A iniciativa *Aleph* foi criada e desenvolvida pela Quanam visando um forte compromisso com a inovação e tem como objetivo promover o crescimento constante de todos os atores de um ecossistema (organizações, PMEs, empresas tradicionais, cidadãos, etc.) por meio da dinamização de suas interações e integrações. Essa dinamização é alcançada através da aplicação de metodologias e ferramentas de TI que criam espaços de oportunidades, permitindo acelerar o ritmo de desenvolvimento de determinada comunidade ou ecossistema.

## **2. Desafio de Negócio**
Em um centro de reabilitação de saúde são instalados sensores para determinar a qualidade das suas condições ambientais. É necessário ter controle da qualidade do ar e outros parâmetros relacionados ao meio ambiente, para agir rapidamente caso sejam detectadas anomalias, que podem ser muito prejudiciais aos pacientes.

Os sensores estão instalados em vários locais como : sala de espera, quartos, banheiros, refeitório, sala de atividades, escritório, jardim.

Os níveis aceitáveis de dados medidos podem variar dependendo da localização do medidor.

Também existem pulseiras que medem a frequência cardíaca, elas são colocadas em pacientes com doenças ou riscos cardíacos. O objetivo é poder controlar e realizar intervenções precoces em pacientes que possuam alterações desses valores.

No escritório, há um servidor disponível para monitoramento dos parâmetros medidos, disponibilizando os níveis dos mesmos em tempo real.

## **3. Objetivo**
Desenvolver uma solução capaz de :
- Capturar dados da central de IoT e persistir os mesmos em algum formato padrão. (por exemplo, arquivo CSV).
- Detectar anomalias em cada uma das séries de dados. O processo deve retornar alertas, dependendo dos valores recebidos dos sensores e do ambiente em que o sensor está localizado.
- Elaborar um modelo que permita prever as condições futuras de uma habitação, com base na análise de dados anteriores. O modelo deverá ser capaz de predizer o ritmo cardíaco de pacientes da habitação que utilizam a pulseira, baseando-se nas condições do ambiente.

## **4. Tecnologias Utilizadas**
Para este desafio, utilizei a linguagem Python com o Jupyter Notebook e também foi utilizado o [Cloud Functions](https://cloud.ibm.com/functions), que é um serviço para execução de funções na nuvem, sem necessidade de um servidor.

## **5. Desenvolvimento da Solução**

### **Parte 1- Alertas de Sensores**
Para a primeira parte, o objetivo era gerar alertas caso as medidas que trabalhamos saíssem do alcance esperado. Para isso, foi realizada a criação de uma API Serverless, utilizando o Cloud Functions.

A API criada deveria receber os seguintes dados, no formato JSON, como no exemplo abaixo :

```json
{
    "room": "bathroom-main",
    "values": {
        "co2": 400,
        "temperature": 22,
        "humidity": 70,
        "sound": 30,
        "illumination": 150
    }
}
```

E retornava um objeto JSON com uma lista das medidas com alertas como no exemplo abaixo :
```json
{
    "alerts": ["temperature", "humidity"]
}
```

Os alertas da lista podem aparecer em qualquer ordem.

Os alcances aceitáveis de valores estão definidos na tabela abaixo:

| Dado                        | Unidade de Medida | Ambiente                             | Alcance de valores aceitáveis    |
| --------------------------- | ----------------- | ------------------------------------ | -------------------------------- |
| CO2 (`co2`)                 | PPM               | Sala de Atividades (`activity-room`) | Até 500                          |
| "                           | "                 | Refeitório (`refectory`)             | Até 400                          |
| "                           | "                 | Quarto 1 (`room-1`)                  | Até 300                          |
| "                           | "                 | Banheiro Principal (`bathroom-main`) | Até 500                          |
| "                           | "                 | Jardim (`garden`)                    | Até 500                          |
| Temperatura (`temperature`) | °C                | Sala de Atividades (`activity-room`) | 19 - 22                          |
| "                           | "                 | Refeitório (`refectory`)             | 20 - 23                          |
| "                           | "                 | Quarto 1 (`room-1`)                  | 21 - 23                          |
| "                           | "                 | Banheiro Principal (`bathroom-main`) | 22 - 25                          |
| "                           | "                 | Jardim (`garden`)                    | 15 - 22                          |
| Humidade (`humidity`)       | %                 | Sala de Atividades (`activity-room`) | 50 - 60                          |
| "                           | "                 | Refeitório (`refectory`)             | 50 - 70                          |
| "                           | "                 | Quarto 1 (`room-1`)                  | 50 - 60                          |
| "                           | "                 | Banheiro Principal (`bathroom-main`) | 60 - 75                          |
| "                           | "                 | Jardim (`garden`)                    | 50 - 80                          |
| Som (`sound`)               | dB                | Sala de Atividades (`activity-room`) | 0 - 40                           |
| "                           | "                 | Refeitório (`refectory`)             | 20 - 35                          |
| "                           | "                 | Quarto 1 (`room-1`)                  | 10 - 30                          |
| "                           | "                 | Banheiro Principal (`bathroom-main`) | 20 - 35                          |
| "                           | "                 | Jardim (`garden`)                    | 10 - 35                          |
| Iluminação (`illumination`) | Lux               | Sala de Atividades (`activity-room`) | 300 - 750                        |
| "                           | "                 | Refeitório (`refectory`)             | 200 - 500                        |
| "                           | "                 | Quarto 1 (`room-1`)                  | 100 - 200                        |
| "                           | "                 | Banheiro Principal (`bathroom-main`) | 100 - 200                        |
| "                           | "                 | Jardim (`garden`)                    | N/A (Qualquer valor é aceitável) |

#### **Solução**
Para solucionar essa questão, realizei a criação de uma ação no Cloud Functions com o Python 3.7 que armazena os valores passados pelo método POST (método de requisição suportado pelo HTTP onde podemos encaminhar dados para serem processados).

Código abaixo utilizado no Cloud Functions :

```python
def main(dict):
    
    values = dict['values']
    room = dict['room']
    
    room_limit = {
        'activity-room' : {'co2' : (0,500), 
                        'temperature' : (19,22), 
                        'humidity' : (50,60), 
                        'sound' : (0,40), 
                        'illumination' : (300,750)
                          },
        
        'refectory' : {'co2' : (0,400), 
                       'temperature' : (20, 23), 
                       'humidity' : (50,70), 
                       'sound' : (20,35), 
                       'illumination' : (200,500)
                      },
        
        'room-1' : {'co2' : (0,300), 
                    'temperature' : (21,23), 
                    'humidity' : (50,60), 
                    'sound' : (10,30), 
                    'illumination' : (100, 200)
                    },
        
        'bathroom-main' : {'co2' : (0,500), 
                           'temperature' : (22,25), 
                           'humidity' : (60,75), 
                           'sound' : (20,35), 
                           'illumination' : (100, 200)
                          },
                          
        'garden' : {'co2' : (0,500), 
                    'temperature' : (15,22), 
                    'humidity' : (50,80), 
                    'sound' : (10, 35)}
    }        
    
    if room == 'garden' :
        del values['illumination']
        
    alarm = [key for key in values.keys() if (values[key] < room_limit[room][key][0]) | (values[key] > room_limit[room][key][1])]
    
    return { 'alerts': alarm }
```

Após realizar a criação do Cloud Functions, podemos utilizar o pacote **requests** para realizar uma requisição à API passando um valor do tipo dicionário para retornar o alarme.

```python
import requests

dict_json = 
{
  "room": "garden",
  "values": {
    "co2": 500,
    "temperature": 24,
    "humidity": 35,
    "sound": 67,
    "illumination": 150
    }
}

# Essa URL podemos encontrar em Terminais dentro do Cloud Functions.
url = ''

# Enviando a requisição POST com os dados do dict_json para a url
r = requests.post(url, json = dict_json)

print(r.json())
# Output : {'alerts': ['humidity', 'sound', 'temperature']}
```

### **Parte 2 - Predição com dados de IoT**
Para esse desafio, a IBM disponibilizou um *broker* MQTT (MQTT, sigla de *Message Queuing Telemetry Transport* é um protocolo de mensagem leve para sensores e pequenos dispositivos móveis). Esse broker capturava dados de sensores IoT em loop, e publicava-os no tópico ```quanam```. No total foram 3200 amostras de dados diferentes, cada uma tendo os valores de co2 (```CO2```), temperatura (```TEMP```), humidade (```HUMID```), som (```SOUND```), iluminação (```ILLUM```) e ritmo cardíaco (```RYTHM```), juntamente com um número identificador da amostra (```ID```), variado de 1 até 3200. O primeiro passado completado foi realizar a captura dos dados do *broker* para então fazer as análises com eles. Abaixo estão as credenciais de acesso para o broker :

```
HOST: iot.maratona.dev
PORT: 31666
USERNAME: maratoners
PASSWORD: btc-2021
```

Para realizar a captura dos dados e a transformação dos dados para ```.csv```, optei por utilizar o pacote ```paho-mqtt``` no Python, mas também encontrei outras opções como utilizar via linha de comando (shell) o pacote ```mosquitto_sub```.

#### **Código utilizando ```paho-mqtt```** :
```python
import paho.mqtt.client as mqtt
import json

def on_connect(client, userdata, flags, rc): #Chamado após utilizarmos client.connect
    print(f"Conectado com o código : {rc}") #Verificar se a conexão funcionou --> 0 = Funcionou
    print("Resgatando os dados do tópico quanam...\n")
    client.subscribe("quanam") #Subscrever no tópico quanam para pegar os dados
    
def on_message(client, userdata, msg):
    message = json.loads(msg.payload.decode()) #Resgatando os dados e passando para o formato json
    data_list.append(message) #Realizando o append para a lista
    
    if len(data_list) == 3200 : #Criando um if para desconectar do client e parar de resgatar os dados
        print("Dados resgatados!")
        client.disconnect() #Desconectar
        print("Realizando a criação do arquivo CSV...")
        pd.DataFrame(data_list).to_csv("data_mqtt.csv", index=False) #Criação de um .csv com os dados capturados
        print("Finalizada a criação do arquivo CSV!")

address = "iot.maratona.dev"
port = 31666
username = "maratoners"
password = "btc-2021"

data_list = [] #Criação de uma lista para armazenar os dados

client = mqtt.Client()
client.on_connect = on_connect
client.on_message = on_message
client.username_pw_set(username=username, password=password) #Setar o usuário e a senha para se conectar e pegar os dados
client.connect(host = address, port = 31666) #Conexão passando o endereço e a porta
client.loop_forever() #Loop para pegar as mensagens, será parado quando entrar no "if" dentro de "on_message"
```

#### **Comando via Shell**
Nesse caso deveríamos verificar uma forma de redirecionar a saída do comando abaixo em um arquivo .txt ou .json para depois ser realizada a transformação em .csv.

```
sudo apt install mosquitto
mosquitto_sub -h iot.maratona.dev -p 31666 -u maratoners -P btc-2021 -t quanam
```

A partir dos dados obtidos via IoT, o nosso objetivo foi realizar uma predição de qual será o ritmo cardíaco de uma pessoa para saber se ela está em risco ou não. Portanto, após o agrupamento dos dados, a tarefa foi realizar um modelo de **regressão**, que era capaz de predizer qual o ritmo cardíaco de um paciente baseando-se nas medidas disponíveis.

## **6. Sobre a Avaliação**
Uma semana após o início do desafio, o sistema de avaliação automática começou as avaliações. O sistema de avaliação utilizou os dados enviados para calcular uma pontuação numérica de 1 até 100, baseada nas respostas de alertas IoT e na métrica R².