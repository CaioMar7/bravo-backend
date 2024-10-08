

# Desafio Técnico: Aplicativo de Autenticação e Gerenciamento de Usuários

Desafio Técnico: Aplicativo de Autenticação e Gerenciamento de Usuários
Você deverá desenvolver uma aplicação web simples que permita a criação e autenticação de usuários. As funcionalidades principais incluem:

Cadastro de usuários.
Login de usuários.
Visualização de um perfil básico após a autenticação.
Requisitos:
Frontend: React.js com TypeScript.
Backend: Node.js (recomendamos o uso de um micro framework, como Express ou Fastify, ou o framework NestJS para maior facilidade no desenvolvimento).
Docker: Configurar dois contêineres (um para frontend e outro para backend).
Prazo e Entrega:
Prazo de entrega: 5 dias úteis após o recebimento deste e-mail.
Repositório GitHub: Faça o upload do código no GitHub e nos envie o link.
Inclua um arquivo README com as instruções para rodar o projeto, incluindo configurações do Docker.

## Tabela de Conteúdos

- [Sobre](#sobre)
- [Tecnologias](#tecnologias)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)


## Sobre

O projeto desenvolvido foi uma aplicação fullstack que possibilita a criação de usuários e autenticação dos mesmos para utilização de rotas públicas e privadas.

## Tecnologias

Liste as principais tecnologias e bibliotecas utilizadas no projeto:

No frontend utilizei: 
- React
- TypeScript
- Tailwind
- ContextAPI
- CustomHooks

No backend utilizei: 
- Node.js
- NestJS
- TypeScript
- Docker
- SQLITE 

## Pré-requisitos

Antes de começar, certifique-se de que você tem os seguintes pré-requisitos instalados em sua máquina:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Node](https://nodejs.org/en/download/package-manager)

## Instalação

Siga as etapas abaixo para instalar o projeto:

1. **Clone o repositório em que se encontra toda a aplicação:**

   ```bash
   git clone https://github.com/CaioMar7/teste-tecnico-bravo
   

### Para instalar o frontend: 

1. Acesse a pasta dentro do diretório principal
   
    ```bash
    cd teste-tecnico-bravo/bravo-frontend 

2. Instale as dependências do projeto:
    
    ```bash
    npm install

3. Configure o arquivo para direcionar as requisições: 
    
    ```bash
    Edite o arquivo src/service/api.ts para apontar para a rota do backend.

### Para instalar o backend:

1. Acesse a pasta dentro do diretório principal

    ```bash
    cd teste-tecnico-bravo/bravo-backend

2. Instale as dependências do projeto:

    ```bash
    npm install

3. Crie um arquivo .env na raiz do projeto e configure com o endereço do banco de dados e a chave secreta JWT. Exemplo:
    
    ```bash
    DATABASE_URL="file:./bravo.db"

    JWT_SECRET=sua_chave_secreta

4. Rode as migrations para criar o banco de dados e as tabelas:
    
    ```bash
    npx prisma migrate dev --name init 
    
5. Para finalizar, rode o build do projeto:

    ```bash
    npm run build


### Para instalar e configurar o Docker e o Docker Compose

Este guia fornece etapas detalhadas para instalar o Docker e o Docker Compose no Windows, além de como executar a aplicação usando o Docker Compose.

### Requisitos

- Sistema Operacional: Windows 10 ou superior (versões Pro, Enterprise ou Education com WSL 2 habilitado).
- Acesso à internet

### Instalação do Docker Desktop

1. Baixar o Docker Desktop:
   - Acesse [Docker Hub](https://www.docker.com/products/docker-desktop) e faça o download do Docker Desktop.

2. Instalar o Docker:
   - Execute o instalador e siga as instruções. Durante a instalação, certifique-se de habilitar o WSL 2 e a integração com o Windows.

3. Iniciar o Docker:
   - Após a instalação, inicie o Docker Desktop. Aguarde até que o Docker esteja em execução (o ícone na bandeja do sistema deve estar ativo).

4. Verificar a instalação:
   - Abra o terminal (cmd ou PowerShell) e execute:

   ```bash
   docker --version

5. Para verificar o Docker Compose **O Docker Compose já vem incluído no Docker Desktop** :

   ```bash
   docker-compose --version


### Para configurar o projeto no Docker

1. A estrutura do seu projeto deve ser semelhante a essa:

    ```bash
    /bravo
    ├── bravo-frontend
    │   └── Dockerfile
    ├── bravo-backend
    │   └── Dockerfile
    └── docker-compose.yml

2. No arquivo docker-compose.yml deve conter a configuração dos containers e para que funcione bem deve seguir a configuração abaixo.
    
    ```bash
        services:
            frontend:
                build:
                context: ./bravo-frontend
                dockerfile: Dockerfile
                ports:
                - "3000:80" 

            backend:
                build:
                context: ./bravo-backend
                dockerfile: Dockerfile
                ports:
                - "3001:3001"
                environment:
                - DATABASE_URL=file:./bravo.db
                volumes:
                - ./bravo-backend/prisma/bravo.db:/app/prisma/bravo.db

3. Explicando as configurações

    ```bash
    frontend:
        build: Indica o contexto e o Dockerfile para construir a imagem do frontend.
        ports: Mapeia a porta 80 do container para a porta 3000 da máquina host.


    backend:
        build: Indica o contexto e o Dockerfile para construir a imagem do backend.
        ports: Mapeia a porta 3000 do container para a porta 3001 da máquina host.
        environment: Configura a variável de ambiente DATABASE_URL para o banco de dados SQLite.
        volumes: Monta o banco de dados SQLite para persistência.

4. Executando o projeto

    Navegue até a pasta onde estão os 2 projetos(frontend e backend) e execute o comando abaixo para inicializar os containers
    
    ```bash
    docker-compose up --build

5. Considerando a configuração acima, o acessar ao frontend e ao backend fica desta forma

    ```bash
    Frontend
    http://localhost:3000



    Backend
    http://localhost:3001
=======
