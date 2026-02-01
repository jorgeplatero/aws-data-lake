# AWS Data Lake - Projeto Boston 311

Este repositório consiste no pipeline de engenharia de dados desenvolvido para a criação de um Data Lake na AWS, realizado durante o treinamento de engenharia de dados na plataforma Alura. O projeto foca na implementação de uma arquitetura medalhão (Bronze, Silver e Gold) para processar dados de solicitações de serviços urbanos da cidade de Boston, transformando dados brutos em insights estratégicos.

### Arquitetura

O diagrama abaixo ilustra a arquitetura do projeto:

<br><p align='center'><img src='https://github.com/jorgeplatero/alura_aws_data_lake/blob/dfb588fdd92f9e76bb7d914ac2d631b7ca5cca01/img/arquitetura.png' alt='Arquitetura AWS Data Lake' width=800></p>

### Pré-requisitos

Certifique-se de possuir uma conta ativa na AWS (Amazon Web Services), o AWS CLI configurado localmente e o Python 3.11+ instalado para execução dos scripts de ingestão.

### Instalação

Clone o repositório:

```bash
git clone https://github.com/jorgeplatero/alura_aws_data_lake.git
```

### Como Rodar a Aplicação

Para executar o pipeline e provisionar a estrutura de dados:

1. Configuração de Credenciais: configure suas chaves de acesso AWS para permitir que o SDK Boto3 interaja com sua conta.

2. Ingestão (Camada Bronze): execute o script Python para realizar o web scraping dos dados do Boston Data Portal e enviá-los ao bucket S3:

```bash
python scripts/ingestao_bronze.py
```

3. Processamento Glue (Camada Silver): no console da AWS, crie e execute o Job do AWS Glue utilizando o script fornecido na pasta `glue/` para realizar a limpeza e padronização dos dados.

4. Processamento EMR (Camada Gold): provisione um cluster EMR e submeta o job Spark para realizar as agregações de negócio, salvando o resultado final em formato Parquet na camada Gold.

5. Visualização: conecte o AWS QuickSight ao bucket S3 (camada Gold) para visualizar o dashboard analítico.

### Tecnologias

| Componente | Tecnologia | Versão | Descrição |
| :--- | :--- | :--- | :--- |
| **Storage** | **AWS S3** | `-` | Armazenamento de objetos para as camadas do Data Lake |
| **Processamento** | **Apache Spark** | `3.x` | Framework de processamento distribuído |
| **ETL & Crawler** | **AWS Glue** | `4.0` | Serviço gerenciado de integração de dados |
| **Big Data Cluster** | **AWS EMR** | `6.x` | Plataforma de cluster gerenciado para Spark |
| **Linguagem** | **Python** | `^3.11` | Linguagem para desenvolvimento de scripts |
| **Visualização** | **AWS QuickSight** | `-` | Ferramenta de BI para criação de dashboards |

### Integrações

O projeto utiliza o **Boto3** para integrar scripts Python locais com o **Amazon S3**. O **AWS Glue** atua na catalogação e transformação inicial, enquanto o **AWS EMR** processa grandes volumes de dados de forma distribuída. A camada final (Gold) é consumida pelo **AWS QuickSight**, que permite a análise das solicitações de melhorias urbanas de Boston.

Link para a fonte de dados: [Boston 311 Service Requests](https://data.boston.gov/dataset/311-service-requests)

Para detalhes sobre a configuração de permissões IAM e políticas de bucket, consulte o treinamento:

Link para o treinamento: [Alura - Engenharia de Dados na AWS](https://www.alura.com.br/)

### Deploy

O deploy da infraestrutura de processamento foi realizado através do console de gerenciamento da AWS, utilizando serviços serverless (Glue) e clusters sob demanda (EMR).
