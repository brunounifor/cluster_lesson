## Estrutura do Projeto

```plaintext
CONTROLE-HSO-KUBERNETES/
├── backend/
│   ├── __init__.py
│   ├── app.py
│   ├── Dockerfile.backend
│   ├── models.py
│   ├── requirements.txt
│   └── routes.py
├── frontend/
│   ├── assets/
│   ├── Dockerfile.frontend
│   ├── index.html
│   ├── script.js
│   └── style.css
├── Dockerfile.postgres
├── README.md
├── backend-deployment.yml
├── backend-service.yml
├── frontend-deployment.yml
├── frontend-service.yml
├── postgres-deployment.yml
└── postgres-service.yml
```
## Pré-requisitos

- Docker
- Kind (Kubernetes in Docker)
- kubectl

## Passo a Passo para Configuração

### 1. Build das Imagens Docker

Primeiro, você deve criar as imagens Docker para cada componente.

#### Backend

Navegue até a pasta `backend` e execute:

```bash
sh ./docker_build.sh
```

#### Frontend

Navegue até a pasta `frontend` e execute:

```bash
sh ./docker_build.sh
```

#### Banco de Dados - MongoDB

Navegue até a pasta `database` e execute:

```bash
sh ./docker_build.sh
```

### 2. Criar um Cluster no Kind

Crie um cluster Kubernetes utilizando `kind`:

```bash
kind create cluster --name todo-list
```

### 3. Carregar as Imagens no Cluster

Para carregar as imagens Docker que você acabou de buildar no cluster `kind`, utilize:

```bash
kind load docker-image cluster-backend:v1 --name todo-list
kind load docker-image cluster-frontend:v1 --name todo-list
kind load docker-image cluster-database:v1 --name todo-list
```

### 4. Aplicar os Deployments e Services

Aplique os arquivos de configuração para o backend, frontend e database:

```bash
kubectl apply -f backend-deployment.yaml
kubectl apply -f backend-service.yaml

kubectl apply -f frontend-deployment.yaml
kubectl apply -f frontend-service.yaml

kubectl apply -f database-deployment.yaml
kubectl apply -f database-service.yaml
```

### 5. Configurar o Port-Forward

Exponha a aplicação de backend utilizando o comando:

```bash
kubectl port-forward service/backend 1997:1997
```
O frontend precisará para comunicar-se com o backend.

Por fim, você pode acessar a aplicação através do serviço frontend utilizando o comando:

```bash
kubectl port-forward service/frontend 8080:3000
```

Agora, você pode acessar a aplicação no navegador através do endereço [http://localhost:8080](http://localhost:8080).