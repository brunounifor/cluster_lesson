__________ Configuração do Projeto Kubernetes: __________

-   Visão Geral do Projeto:
    O projeto está organizado nas seguintes pastas e arquivos principais:

    ```plaintext
    CLUSTER_LESSON/
    ├── backend/
    │   ├── controllers/
    │   ├── models/
    │   ├── routes/
    │   ├── index.js
    │   ├── backend-deployment.yaml
    │   ├── backend-service.yaml
    │   └── Dockerfile
    ├── frontend/
    │   ├── public/
    │   ├── src/ 
    │   │   ├── componentes/
    │   │   └── service/
    │   ├── App.js
    │   ├── index.css
    │   ├── index.js
    │   ├── Dockerfile
    │   ├── frontend-deployment.yaml
    │   └── frontend-service.yaml
    └── database/
        ├── Dockerfile
        ├── db-deployment.yaml
        └── db-service.yaml
    ```

-   Ferramentas Necessárias:
    Para rodar esse projeto, você precisa garantir que tem as seguintes ferramentas instaladas no seu ambiente:

        * Docker: para construir e rodar as imagens
        * Kind: para gerenciar o cluster Kubernetes
        * kubectl: para interagir com o cluster Kubernetes

__________ Guia de Configuração: __________

-   Etapa 1. Construção das Imagens Docker:
    Cada parte do projeto requer a criação de imagens Docker. Abaixo estão os comandos que você deve executar dentro das respectivas pastas:

        * Database:
            sh ./docker_build.sh
        * Frontend:
            sh ./docker_build.sh
        * Backend: 
            sh ./docker_build.sh

-   Etapa 2. Criação do Cluster Kubernetes:

    Crie um cluster Kubernetes com o nome todo-list usando o Kind, com o seguinte comando:
        kind create cluster --name todo-list

-   Etapa 3. Carregar Imagens no Cluster:
    Com as imagens Docker prontas, o próximo passo é carregá-las no cluster Kubernetes que você acabou de criar. Para isso, utilize os comandos a seguir:

        kind load docker-image cluster-database:v1 --name todo-list
        kind load docker-image cluster-frontend:v1 --name todo-list
        kind load docker-image cluster-backend:v1 --name todo-list


-   Etapa 4. Aplicar Configurações Kubernetes:
    Agora, aplique os arquivos de configuração para cada parte do sistema (backend, frontend e banco de dados). Execute os comandos conforme mostrado abaixo:

        * Database:
            kubectl apply -f db-deployment.yaml
            kubectl apply -f db-service.yaml
        * Frontend:
            kubectl apply -f frontend-deployment.yaml
            kubectl apply -f frontend-service.yaml
        * Backend: 
            kubectl apply -f backend-deployment.yaml
            kubectl apply -f backend-service.yaml

-   Etapa 5. Exposição dos Serviços:
    Para acessar os serviços localmente, você precisará usar o comando port-forward para mapear as portas. Siga as instruções abaixo:

        * Backend:
            kubectl port-forward service/backend 1997:1997
        * Frontend:
            kubectl port-forward service/frontend 8080:4173

Pronto! Se todos os passos tiverem sido executados corretamente, a aplicação está configurada e rodando localmente no Kubernetes.
Agora, você pode abrir seu navegador e acessar a aplicação através de http://localhost:8080.