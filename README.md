# 💡 Smart Lamp - FIWARE

Projeto desenvolvido para o **Checkpoint 4** da disciplina de Edge Computing da FIAP.

A solução utiliza um **ESP32**, um sensor **LDR** e a plataforma **FIWARE** para realizar comunicação entre dispositivo IoT e nuvem, permitindo o envio de dados de luminosidade e o controle remoto do LED onboard.

## 👥 Autores

- Bruno Gonçalves Minitti
- Nicolas Gomes de Almeida
- Lucas Rodrigues

## 🚀 Funcionalidades

- Leitura de luminosidade através de sensor LDR
- Envio dos dados de luminosidade para o FIWARE
- Consulta dos dados através do Orion Context Broker
- Controle remoto do LED onboard do ESP32
- Comandos `on` e `off` enviados através do Postman
- Comunicação utilizando MQTT
- Simulação completa através do Wokwi

## 🛠️ Tecnologias utilizadas

- ESP32 DEVKIT V1
- LDR
- C/C++ / Arduino
- MQTT
- FIWARE
- Orion Context Broker
- IoT Agent
- Eclipse Mosquitto
- STH-Comet
- MongoDB
- Docker
- AWS EC2
- Postman
- Wokwi

## 🔄 Fluxo da solução

### Edge → Cloud

```text
LDR
 ↓
ESP32
 ↓
MQTT
 ↓
Mosquitto
 ↓
IoT Agent
 ↓
Orion Context Broker
```

O ESP32 realiza a leitura da luminosidade através do sensor LDR e envia o valor para o FIWARE utilizando MQTT.

### Cloud → Edge

```text
Postman
 ↓
Orion Context Broker
 ↓
IoT Agent
 ↓
MQTT
 ↓
ESP32
 ↓
LED
```

Os comandos enviados pelo Postman permitem ligar e desligar remotamente o LED onboard do ESP32.

## 📡 Entidade FIWARE

A Smart Lamp foi configurada com os seguintes dados:

```text
Device ID: lamp001
Entity: urn:ngsi-ld:Lamp:001
Type: Lamp
Transport: MQTT
```

### Atributos

| Atributo | Tipo | Descrição |
|---|---|---|
| `state` | Text | Estado atual do LED (`on` ou `off`) |
| `luminosity` | Integer | Valor de luminosidade obtido pelo LDR |

### Comandos

| Comando | Função |
|---|---|
| `on` | Liga o LED onboard |
| `off` | Desliga o LED onboard |

## ☁️ Infraestrutura FIWARE

O FIWARE foi executado em uma instância **AWS EC2** utilizando containers Docker.

Os principais componentes utilizados foram:

- Orion Context Broker
- IoT Agent
- Eclipse Mosquitto
- MongoDB
- STH-Comet

Antes da integração com o ESP32, foram realizados Health Checks dos principais serviços para validar o funcionamento da infraestrutura.

### Health Checks utilizados

```text
Orion Context Broker
GET /version
Porta: 1026

IoT Agent
GET /iot/about
Porta: 4041

STH-Comet
GET /version
Porta: 8666
```

## 📊 Comunicação MQTT

O dispositivo utiliza MQTT para realizar a comunicação com o FIWARE.

Principais tópicos utilizados:

```text
/TEF/lamp001/cmd
/TEF/lamp001/attrs
/TEF/lamp001/attrs/l
```

- `/cmd` recebe comandos enviados pelo FIWARE
- `/attrs` envia o estado atual do LED
- `/attrs/l` envia o valor de luminosidade

## 🎮 Simulação no Wokwi

A simulação completa do projeto pode ser acessada em:

https://wokwi.com/projects/475450974077827073

Na simulação é possível:

- visualizar a leitura do sensor LDR
- acompanhar os dados pelo Serial Monitor
- enviar dados de luminosidade ao FIWARE
- receber comandos `on` e `off`
- ligar e desligar o LED onboard remotamente

## 📁 Código

O código principal do projeto está disponível no arquivo:

```text
smart_lamp_fiware.ino
```

O código realiza:

- conexão com Wi-Fi
- conexão com o broker MQTT
- leitura do sensor LDR
- publicação dos dados de luminosidade
- publicação do estado do LED
- recebimento dos comandos `on` e `off`

## ✅ Testes realizados

Foram validados os dois fluxos de comunicação da solução.

### Edge → Cloud

O ESP32 envia o valor do LDR para o FIWARE e o dado pode ser consultado através do Postman.

Exemplo:

```json
{
  "type": "Integer",
  "value": 24
}
```

### Cloud → Edge

O Postman envia comandos ao FIWARE, que são encaminhados ao ESP32 através de MQTT.

```text
on  → LED ligado
off → LED desligado
```

O estado atualizado também pode ser consultado através do Orion Context Broker.

## 🎓 Contexto acadêmico

Projeto desenvolvido para fins acadêmicos no **Checkpoint 4 de Edge Computing da FIAP**, com foco em IoT, computação em nuvem, MQTT e integração com a plataforma FIWARE.
