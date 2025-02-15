# Projeto de experiência com Kafka para fins de estudo

## Arquitetura do Kafka

O Kafka é uma plataforma de streaming distribuída que funciona como um intermediário de mensagens, facilitando a troca de dados entre produtores e consumidores em tempo real. Ele opera com base no modelo de publicação e assinatura (publish-subscribe) e é utilizado para construir pipelines de dados em tempo real e aplicativos de streaming. Os principais componentes do Kafka são:

- Produtor (Producer): Um cliente que envia mensagens para um tópico do Kafka. O produtor publica dados no cluster do Kafka.
- Consumidor (Consumer): Um cliente que lê mensagens dos tópicos do Kafka. Os consumidores assinam tópicos e processam os dados.
- Tópicos (Topics): Canais lógicos onde os produtores enviam mensagens e de onde os consumidores as leem. Cada tópico pode ter várias partições, permitindo que o Kafka paralelize o processamento entre consumidores.
- Broker: Um servidor que armazena e entrega mensagens. O Kafka é projetado para ser distribuído, permitindo a configuração de múltiplos brokers para escalabilidade e tolerância a falhas.
- Zookeeper: Coordena os brokers do Kafka, mantendo o controle dos tópicos, partições e deslocamentos (offsets) das mensagens.

## O Projeto de exemplo

O projeto consiste em dois Consumers e um Producer, simulando um sistema de pedidos. Quando o endpoint "/orders" recebe um POST com o JSON do tipo
```
{
"name":"Vinicius1",
"description":"compra1",
"amount":150.10
}
```

É disparada uma mensagem pelo Producer para os Consumers. A dinâmica de envio para o producer 1 ou 2 pode ser ajustada à vontade, colocando um load balancer, por exemplo,
para melhorar a efetividade do processamento.

Após o recebimento da mensagem pelo Consumer, pode ser criada a lógica para atender as necessidades do projeto: enviar um e-mail, acionar o sistema de estoque,
acionar o sistema de confirmação de pagamento e etc.

## Instruções para executar o projeto

A maneira mais fácil de iniciar o Kafka seria por uma imagem Docker. Caso tenha o Docker instalado na sua máquina, pode rodar os seguintes comandos no terminal:
```
sudo docker pull apache/kafka:3.7.1 # esse comando vai baixar a imagem do Kafka
```

Logo após, vamos iniciar o Kafka na porta 9092:
```
sudo docker run -p 9092:9092 apache/kafka:3.7.1
```
Uma vez que o Kafka esteja ativo, basta clonar o projeto para sua máquina e executar com uma IDE de sua escolha.

Depois que o Producer e os Consumers estejam rodando, juntamente com o servidor do Kafka rodando no Docker, basta enviar um comando post para o endpoint "/orders".
A maneira mais simples é usar o cURL, mas caso queira, pode usar o Postman ou Insomnia para isso.
``` 
curl -X POST -H "Content-Type: application/json" -d '{"name":"Farofa","description":"compra1","amount":15.10}' localhost:8081/orders
```

