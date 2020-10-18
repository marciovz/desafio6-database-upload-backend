
# DESAFIO6 - Database - Upload - Backend

## Visão geral
Desafio6 Database - Upload é um servidor backend para serviços de gerenciamento de transações financeiras, uma continuação da implementação do desafio 5, adicionando o armazenamento em banco de dados e upload de arquivos.

A aplicação é uma resolução do desafio 6 módulo 2 do curso Bootcamp da Rocketseat para aplicação dos conhecimentos adiquiridos sobre backend com nodeJS, banco de dados utilizando ORM, e upload de arquivos utilizando a biblioteca multer.

O backend desta aplicação será responsável pelo armazenamento dos valores de depósito e retirada, gerenciando esse valores e controlando o saldo atual, e as transações permitidas.

O desafio é composto pela construção de um servidor em NodeJS utilizando a linguagem typescript. O projeto possui uma estrutura de pastas divididas por responsabilidades como, models, repositories, routes e services.
Os dados serão armazenados em um banco de dados postgres utilizando a typeorm.
Foi implementado o upload de arquivo, permitando subir arquivos csv e adicionar uma listagem de transações automaticamente no sistema.

### Funcionalidades
- listagem das transações efetuadas e o saldo;
- criar uma transação do tipo income para entrada de um valor;
- criar uma transação do tipo outcome para retirada de um valor;
- criar transações através de importação de arquivos csv;
- excluir uma transação;
- controle sobre o saldo, restringindo retiradas resultantes em saldo negativo;


### Bibliotecas
- express: utilizada para criação de um servidor;
- typescript: permite escrevermos código typescript para rodar no nodeJS;
- ts-node-dev: utilizado para inicialização e monitoramento de alterações nos arquivos typescript;
- jest: utilizado para testes unitários na aplicação;
- supertest: utilizado para testes da aplicação;
- cors: utilizado para controle de acesso de domínios externos;
- csv-parse: utilizado para converter arquivos csv;
- multer: utilizado para importação de arquivos via requisição;
- pg: plugin de acesso ao banco de dados postgres;

### Implementações
- Implementado com typescript;
- servidor usando express;
-


<br />

## Instalação

### 1. Requisitos para instalação e rodar a aplicação
- NodeJS na versão 8 ou superior;
- yarn ou npm;
- curl, postman ou insomnia.
- Banco de dados postgres instalado.

### 2. Download

Clonar a pasta do projeto para sua máquina local e instalar as dependências.
```bash
 # clonar o repositório
 $ git clone https://github.com/marciovz/desafio6-database-upload-backend.git

 # acessar a pasta backend
 $ cd desafio6-database-upload-backend

 # instalar as dependências do projeto
 $ yarn
```
### 3. Configurar o banco de dados
  No arquivo ormconfig.json, dentro da raiz do projeto, configurar dados conforme seu banco de dados:
  **ormconfig.json**
  ```code
    "host": "localhost",
    "port": 5432,
    "username": "seu_user",
    "password": "seu_password",
    "database": "nome_do_seu_banco",
  ```

### 5. Rodar a migração para criação das tabelas
```bash
$ yarn typeorm migration:run
```

### 4. Iniciando o servidor
```bash
$ yarn dev:server
```

<br />

## Usando os serviços

Abaixo temos as linhas de comandos para fazer as requisições através dos comandos curl em seu terminal, mas você também pode utilizar um aplicativo como postman ou insomnia para executar as requisições ao servidor.

 ### Criar uma transação do tipo deposito (income)
```bash
$ curl -H "Content-Type: application/json" -X POST -d '{"title": "Salário" , "value": 3000, "type": "income", "category": "Renda Fixa"}' http://localhost:3333/transactions
```
<br />

 ### Criar uma transação do tipo deposito (outcome)
```bash
$ curl -H "Content-Type: application/json" -X POST -d '{"title": "IPTU" , "value": 800, "type": "outcome", "category": "Impostos"}' http://localhost:3333/transactions
```
<br />

 ### Listar todas transações e o mostra o salto atual.
```bash
$ curl -H "Content-Type: application/json" -X GET http://localhost:3333/transactions
```
<br />

 ### Excluir uma transações passando seu id.
```bash
$ curl -H "Content-Type: application/json" -X DELETE http://localhost:3333/transactions/ID_TRANSAÇÃO
```
<br />

 ### Upload de arquivo csv.
 Atenção:
 Substitua o caminho myUser/path/ com o nome do caminho onde você fez o clone do projeto.
 Mantenha o caractere @ no inicio do caminho como abaixo.

```bash
$ curl -H "Content-Type: multipart/form-data" -X POST -F "file=@myUser/path/desafio6-database-upload-backend/arquivo_teste.csv" http://localhost:3333/transactions/import
```
<br />

