# Zephyr Producer

## Descrição

O **Zephyr Producer** é um microserviço desenvolvido em **Java 17** com **Spring Boot**, responsável por ler arquivos `.csv` e produzir mensagens para o **Apache Kafka**. Essas mensagens podem ser consumidas diretamente por um consumidor tradicional ou pelo **Kafka Connect**, permitindo a persistência dos dados no **PostgreSQL**.

Este repositório faz parte da plataforma **[Zephyr Platform](https://github.com/marcuslira2/zephyr-platform)**, que compara abordagens diferentes de processamento de dados com Kafka.

---

## 🚀 Funcionalidades

- Leitura de arquivos **CSV**.
- Publicação de mensagens no **Kafka**.
- Suporte a diferentes formatos de mensagens (padrão consumidor ou Kafka Connect).
- Configuração flexível via `application.yml`.
- Monitoramento e logging estruturado.

---

## 📌 Tecnologias Utilizadas

- **Java 17**
- **Spring Boot** (Web, Kafka, Config)
- **Apache Kafka**
- **Docker**
- **Maven**

---

## 📂 Estrutura do Projeto

```
zephyr-producer/
├── src/
│   ├── main/
│   │   ├── java/com/zephyr/producer/
│   │   │   ├── config/      # Configurações do Kafka e Spring Boot
│   │   │   ├── service/     # Serviço de leitura e publicação de mensagens
│   │   │   ├── controller/  # Endpoints REST
│   │   │   ├── dto/         # Estruturas de dados
│   │   ├── resources/
│   │   │   ├── application.yml  # Configuração do projeto
│   ├── test/                 # Testes unitários
├── Dockerfile                # Dockerização do serviço
├── pom.xml                   # Dependências do projeto
```

---

## ⚙️ Configuração

### 📌 Variáveis de Ambiente

O `application.yml` deve ser configurado para apontar para o broker Kafka correto:

```yaml
spring:
  kafka:
    bootstrap-servers: kafka:9092
    producer:
      key-serializer: org.apache.kafka.common.serialization.StringSerializer
      value-serializer: org.apache.kafka.common.serialization.StringSerializer
```

Outros parâmetros podem ser ajustados conforme necessidade.

---

## 🛠 Como Rodar o Projeto

### 🔧 Executando Localmente

1. Clone o repositório:
   ```bash
   git clone https://github.com/marcuslira2/zephyr-producer.git
   ```
2. Entre na pasta do projeto:
   ```bash
   cd zephyr-producer
   ```
3. Execute o Maven para compilar e rodar:
   ```bash
   mvn spring-boot:run
   ```

### 🐳 Executando com Docker

1. Compile o projeto:
   ```bash
   mvn clean package
   ```
2. Construa a imagem Docker:
   ```bash
   docker build -t zephyr-producer .
   ```
3. Execute o contêiner:
   ```bash
   docker run --network=minha_rede -p 8080:8080 zephyr-producer
   ```

---

## 📡 Endpoints Disponíveis

### 1️⃣ Enviar Arquivo CSV para Processamento
```http
POST /api/producer/upload
```
**Corpo da requisição:** `multipart/form-data`

**Resposta esperada:**
```json
{
  "message": "Arquivo processado com sucesso.",
  "totalRecords": 1000
}
```

### 2️⃣ Enviar Dados JSON Manualmente
```http
POST /api/producer/send
```
**Corpo da requisição:**
```json
{
  "id": 1,
  "nome": "Produto X",
  "preco": 99.99
}
```

---

## 📜 Licença

Este projeto está sob a licença **MIT**. Sinta-se livre para usar, modificar e contribuir!

---

## 📫 Contato
Caso tenha alguma dúvida ou sugestão, entre em contato via [GitHub Issues](https://github.com/marcuslira2/zephyr-producer/issues).

