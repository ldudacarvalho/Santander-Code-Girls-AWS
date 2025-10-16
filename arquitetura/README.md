# 💡 Projeto 01: Pipeline de Pós-Produção de Imagens de Alto Volume

Este projeto aborda a necessidade de um estúdio de fotografia de processar arquivos **RAW de alta resolução** de forma **eficiente e segura**, resolvendo dois desafios principais:  
- 💰 **Alto custo de servidores potentes**  
- 🔒 **Entrega insegura de arquivos finais**

A arquitetura final é uma solução **robusta e escalável**, utilizando **Orquestração Serverless** para garantir que o poder de computação seja pago apenas quando necessário e que a entrega ao cliente seja rápida e protegida.

---

## 🚀 1. A Ideia Central — Otimização de Custos e Poder sob Demanda

A ideia por trás desta arquitetura é transformar o servidor caro de edição (**EC2**) em um **recurso de uso sob demanda**.

### 🧩 Problema do Negócio
Um estúdio de fotografia precisava de um servidor potente para o processamento de imagens (que exige alta CPU), mas esse servidor ficava a maior parte do tempo ocioso.  
Manter um EC2 ligado **24/7** gerava um custo desnecessário.

### 🧠 Solução — Lambda como Gerente de Custos
Em vez de manter o EC2 ligado, usamos o **Lambda Orquestrador** para ligar o EC2 **apenas no momento exato em que um novo arquivo é detectado no S3**.  

O Lambda atua como um **“gerente”**, que:
- Dispara o trabalho automaticamente.
- Permite que o EC2 se desligue após o processamento.
- Garante que o estúdio pague **somente pelos minutos de computação utilizados**.

---

## ⚙️ 2. Detalhamento Técnico do Fluxo de Trabalho

A solução é dividida em **três fases interconectadas**, conforme ilustrado no diagrama da arquitetura.

---

### 🟣 **Fase I — Ingestão e Acionamento**
O processo começa com o **upload e o acionamento automático** do pipeline:

1. **Entrada Segura:**  
   O fotógrafo inicia o processo fazendo o upload da foto, que atravessa a Internet e chega ao ambiente AWS via **API Gateway**.

2. **Armazenamento RAW:**  
   A imagem é salva no **S3 (Bucket RAW)**.

3. **Gatilho de Evento:**  
   O upload no S3 atua como um **trigger**, disparando a função **Lambda Orquestrador**.

4. **Orquestração:**  
   O Lambda executa duas tarefas essenciais:
   - 🧾 **Registro:** Grava o novo job no **Banco de Dados (DynamoDB/RDS)** com status “Pendente”.  
   - ⚡ **Inicia o EC2:** Envia o comando para ligar a instância **EC2**, passando os parâmetros do arquivo.

5. **Recurso de Disco:**  
   O volume **EBS** (armazenamento de alta performance) é montado no EC2 para manipulação eficiente de arquivos grandes.

---

### 🟢 **Fase II — Processamento Pesado (O “Músculo”)**
O controle é transferido para a instância dedicada **EC2**, que executa o trabalho intensivo:

1. **Leitura de Dados:**  
   O EC2 lê o arquivo RAW diretamente do **S3 (Bucket RAW)**.

2. **Execução:**  
   O software de edição processa a imagem (redimensionamento, correção de cor, etc.), utilizando o poder de CPU e disco **EBS**.

3. **Armazenamento Final:**  
   As imagens processadas são salvas no **Bucket final_Processado**.

4. **Finalização:**  
   O EC2 atualiza o status do job para **Concluído** no Banco de Dados e **é desligado automaticamente**, economizando recursos.

---

### 🔵 **Fase III — Entrega e Download Seguro**
A etapa final garante a **entrega protegida** das imagens ao cliente:

1. **Solicitação:**  
   O cliente solicita o download da imagem final via **API Gateway**.

2. **Serviço de Download:**  
   O API Gateway aciona o **Lambda Download Service**.

3. **Verificação:**  
   O Lambda consulta o **Banco de Dados** para confirmar se o job está “Concluído” e se o cliente possui permissão.

4. **Geração de Link:**  
   O Lambda gera uma **URL Pré-assinada** no S3 (link temporário e seguro).

5. **Download Direto:**  
   O cliente baixa o arquivo diretamente do **S3**, via **HTTPS**, sem sobrecarregar a API ou o Lambda.

---

## 🧾 3. Conclusão Técnica

O diagrama final demonstra **excelência em arquitetura de nuvem**, combinando:
- 🔐 **API Gateway** como fronteira segura de entrada.  
- ⚙️ **Lambda** como orquestrador inteligente.  
- 🖥️ **EC2 + EBS** fornecendo poder de processamento sob demanda.  
- 🪣 **S3** como armazenamento central e mecanismo de entrega.  
- 🗄️ **Banco de Dados** garantindo rastreabilidade e controle do pipeline.  

Essa abordagem entrega **eficiência, segurança e custo otimizado**, ideal para ambientes de **alta carga de processamento** com uso esporádico.

---



