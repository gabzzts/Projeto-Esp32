
# Sistema de Monitoramento e Controle de Uso de Água

## Descrição

Este projeto visa desenvolver um sistema de monitoramento e controle do uso de água utilizando sensores de umidade e uma bomba acionada por um relé, com comunicação via MQTT. O sistema pode ser utilizado em ambientes industriais ou para consumo doméstico, com o objetivo de otimizar o uso de água e detectar vazamentos. A solução é baseada em um microcontrolador ESP32, sensores de umidade, e um servidor MQTT para enviar e receber dados em tempo real.

### Funcionalidades
- Monitoramento contínuo da umidade do solo (ou área em questão).
- Ação de controle da bomba com base na leitura da umidade.
- Detecção de vazamentos (bomba desligada quando a umidade está muito baixa).
- Publicação de dados de umidade e status da bomba em tempo real para o broker MQTT.
- Controle manual via tópicos MQTT para ligar ou desligar a bomba.

## Tecnologias Utilizadas
- **ESP32**: Microcontrolador utilizado para captar os dados dos sensores e controlar os atuadores.
- **Sensor de Umidade YL-69**: Sensor utilizado para medir a umidade do ambiente.
- **MQTT**: Protocolo de mensagens utilizado para a comunicação entre o dispositivo e a plataforma de controle.
- **PubSubClient**: Biblioteca MQTT para ESP32 para facilitar a comunicação.
- **WiFi**: Conexão Wi-Fi para comunicação com o broker MQTT.

## Como Funciona

### Funcionamento do Sistema

1. O sensor de umidade monitora constantemente a umidade do ambiente.
2. A bomba é controlada automaticamente, com base na leitura da umidade. Se a umidade for baixa, a bomba é ligada para irrigar. Se a umidade for alta, a bomba é desligada.
3. O valor da umidade é enviado periodicamente para um broker MQTT, onde pode ser monitorado em tempo real.
4. O sistema também permite o controle manual da bomba através de comandos enviados via MQTT.

### Tópicos MQTT

- **Tópicos de publicação**:
  - `gabriel/agua/umidade`: Envia o valor da umidade do ambiente.
  - `gabriel/agua/status`: Envia o status atual da bomba (se está ligando ou desligada).

- **Tópicos de assinatura**:
  - `gabriel/agua/controle`: Comandos para controlar manualmente a bomba (exemplo: `ligar`, `desligar`, `auto`).

## Como Usar

### 1. Conectar o ESP32 à rede Wi-Fi

Edite o código para inserir os dados da sua rede Wi-Fi:

const char* ssid = "NOME_DA_SUA_REDE";            // Substitua pelo nome da sua rede Wi-Fi
const char* password = "SUA_SENHA_WIFI";          // Substitua pela senha da sua rede Wi-Fi

const char* mqtt_server = "test.mosquitto.org";  // Broker MQTT público
const int mqtt_port = 1883;                      // Porta padrão MQTT

#2. Carregar o código no ESP32:

Conecte o ESP32 ao seu computador via USB.
Abra o Arduino IDE e selecione a placa ESP32 Dev Module.
Carregue o código para o ESP32.

#3. Acompanhar as leituras e o controle:
Os dados de umidade e status da bomba serão enviados periodicamente para o broker MQTT. Você pode monitorar os valores através de um cliente MQTT, como o MQTT Explorer, ou criar um frontend para visualizar e controlar o sistema.

#4.Controle manual
Para controlar manualmente a bomba, envie um comando para o tópico gabriel/agua/controle:

Enviar ligar para ligar a bomba.
Enviar desligar para desligar a bomba.
Enviar auto para voltar ao controle automático.

# Requisitos
Arduino IDE com suporte para ESP32.
Bibliotecas:
WiFi.h: Para conectar o ESP32 à rede Wi-Fi.
PubSubClient.h: Para comunicação MQTT.
Para instalar a biblioteca PubSubClient:

Abra o Arduino IDE.
Vá em Sketch > Incluir Biblioteca > Gerenciar Bibliotecas.
Pesquise por PubSubClient e instale.
