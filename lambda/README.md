# 🚀 Automação com AWS Lambda e S3

## 📋 Sobre o Desafio

Este projeto documenta minha jornada de aprendizado sobre automação de tarefas utilizando **AWS Lambda** e **Amazon S3**, focando na arquitetura e conceitos de integração entre serviços serverless da AWS.

## 🎯 Objetivo do Projeto

Consolidar conhecimentos em:

- Integração entre **S3** e **Lambda Functions**
- Arquitetura de sistemas **serverless**
- **Documentação técnica** no GitHub
- **Processos de automação** na AWS

## 🏗️ Arquitetura Proposta

![Diagrama de Arquitetura](https://../images/lambda5.jpg)

### Fluxo da Arquitetura

#### 📤 Upload → 🗂️ **Amazon S3** → ⚡ **Trigger** → 🏗️ **AWS Lambda** → 💾 **DynamoDB**
                                                         |
#### 🔍 Consulta ← 🌐 **API Gateway** ← 🏗️ **AWS Lambda** ← 💾 **DynamoDB**

## Componentes Explicados

### 🔄 Fluxo de Upload (Escrita)

1. O usuário sobe um arquivo no **S3**.
2. O **Trigger S3** detecta automaticamente o novo arquivo.
3. A **Lambda** é acionada para processar o arquivo.
4. **DynamoDB** armazena os dados processados.

### 🔍 Fluxo de Consulta (Leitura)

1. O **Postman** (cliente) envia uma requisição para o **API Gateway**.
2. O **API Gateway** rota para a **Lambda**.
3. A **Lambda** consulta os dados no **DynamoDB**.
4. A resposta retorna via **API Gateway** para o **Postman**.

---

## 🤔 Por Que Usar LocalStack?

### O Que é LocalStack?
LocalStack é uma ferramenta que simula serviços AWS localmente, permitindo desenvolvimento e testes sem custos na nuvem real.

### Vantagens para Este Projeto:

- 🏠 **Desenvolvimento Local**: Testar integrações S3-Lambda offline.
- 💰 **Economia de Custos**: Evitar cobranças da AWS durante desenvolvimento.
- 🚀 **Agilidade**: Iterações rápidas sem deploy na nuvem.
- 🧪 **Testes Isolados**: Ambiente controlado para experimentos.

---

## ⚡ O Que é AWS Lambda?

### Definição
**AWS Lambda** é um serviço de computação serverless que executa código em resposta a eventos, sem a necessidade de provisionar ou gerenciar servidores.

### Características Principais:

- ✅ **Serverless**: Sem gerenciamento de infraestrutura.
- ✅ **Escalável**: Processa de 1 a milhares de eventos simultaneamente.
- ✅ **Pago por Uso**: Cobrança apenas pelo tempo de execução.
- ✅ **Multi-Linguagem**: Suporte a Python, Node.js, Java, etc.

### 🔗 Relação Lambda-S3 em Tarefas Automatizadas

#### Como Funciona a Integração?
- **S3 como Disparador**: Eventos do S3 (upload, delete) disparam Lambdas.
- **Processamento Automático**: Arquivos são processados assim que chegam no S3.
- **Pipeline de Dados**: Criação de fluxos ETL (Extract, Transform, Load).

#### Casos de Uso Comuns:
- 📊 **Processamento de Logs**: Analisar arquivos de log automaticamente.
- 🖼 **Redimensionamento de Imagens**: Processar imagens no upload.
- 📈 **ETL de Dados**: Transformar dados CSV/JSON para análise.
- 🔒 **Validação de Arquivos**: Verificar integridade e segurança.

---

## 🛠️ Ferramentas Utilizadas

- **Diagramação**:
  - Draw.io: Para criação de diagramas de arquitetura.
  - Linguagem de Markdown: Documentação técnica.
- **Serviços AWS**:
  - **Lambda**: Processamento serverless.
  - **S3**: Armazenamento de objetos.
  - **DynamoDB**: Banco de dados NoSQL.
  - **API Gateway**: Interface de API.

---

## 💡 Insights e Aprendizados

### Arquiteturais:
- A integração **S3-Lambda** cria pipelines de dados altamente escaláveis.
- Arquitetura **serverless** reduz custos operacionais.
- **Triggers automáticos** eliminam a necessidade de polling.

### Técnicos:
- Importância do **tratamento de erros** em funções Lambda.
- Estratégias para lidar com **grandes volumes de arquivos**.
- **Monitoramento via CloudWatch** para debugging.

---

## 📚 Próximos Passos

### Melhorias Futuras:
- Implementar a arquitetura com código real.
- Adicionar **monitoramento e alertas**.
- Implementar **testes automatizados**.
- Adicionar **autenticação na API**.

### Expansões Possíveis:
- Processamento de diferentes tipos de arquivo.
- Integração com mais serviços AWS (SNS, SQS).
- **Dashboard** para visualização de dados.

---

## 🔗 Recursos Úteis

- [Documentação AWS Lambda](https://aws.amazon.com/lambda/)
- [Documentação Amazon S3](https://aws.amazon.com/s3/)
- [LocalStack Documentation](https://docs.localstack.cloud/)

---
