# Trabalho Prático - Ciclo 02: Conteinerização de Aplicação

Este repositório contém a entrega do trabalho prático de Sistemas Distribuídos (Conteinerização de Aplicação).

## Membros do Grupo
* 1. Amábile Honorato Zucchetti - Matricula: 2310438
* 2. André Marcos de Sousa Tavares - Matricula: 2313280 
* 3. Gabriel Pedro Silva Dutra - Matricula: 2310154 
* 4. Guilherme Poloniato Salomão - Matricula: 2310359
* 5. Matheus Sabino Ribeiro - Matricula: 2313148
---

## Passo a Passo para Execução (Comandos Docker)

Siga os comandos abaixo na ordem para construir as imagens e iniciar os containers corretamente. Todos os comandos devem ser executados na raiz deste projeto.

### 1. Criar a rede customizada do projeto
Precisamos criar uma rede no Docker para que os containers possam se encontrar e se comunicar pelo nome.

```bash
docker network create tarefas-network
```

### 2. Fazer o build das imagens
Construindo a imagem do Backend:

```bash
docker build -t backend-img ./backend
```

Construindo a imagem do Frontend:
```bash
docker build -t frontend-img ./frontend
```

### 3. Rodar o container do Banco de Dados
Iniciando o Banco de dados - PostgreSQL:

```bash
docker run -d --name postgres --network tarefas-network -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=secret -e POSTGRES_DB=tarefasdb -p 5432:5432 postgres:latest
```

### 4. Rodar o container do Backend
Iniciando a API do container backend:

```bash
docker run -d --name backend --network tarefas-network -e DB_HOST=postgres -e DB_USER=postgres -e DB_PASSWORD=secret -e DB_NAME=tarefasdb -e PORT=4000 -p 4000:4000 backend-img

```

### 5. Rodar o container do Frontend
Iniciando o container do Frontend:

```bash
docker run -d --name frontend --network tarefas-network -p 8080:8080 frontend-img
```

---

## 6 Acessando a Aplicação
Após executar todos os passos, a aplicação estará disponível em:
* **Frontend:** http://localhost:8080
* **Backend (API):** http://localhost:4000