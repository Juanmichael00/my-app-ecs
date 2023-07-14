# Sample application with ECS  🐋
## Autor: Juan M.
Neste tutorial aprenderemos a subir uma aplicação simples em Docker no ECS: Criação da imagem docker, repositório privado ECR, push da imagem para o repositório, criação do cluster ECS Fargate, task definition, service e exporemos nossa aplicação para a internet...
---

## Passo a passo

### 1 - Clone o repositório: 
https://github.com/Juanmichael00/my-app-ecs.git

### 2 - Configure uma chave CLI
https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html

### 3 - Instale o Docker  (linux/Ubuntu)
```
sudo apt-get update

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
### 4 - Crie um usuário com acesso programático com as devidas permissões para acessar o ecs, ecr, ec2... (ou use a policy administrator-access, mas cuidado!!!)

### 5 - Recupere um token de autenticação e autentique seu cliente Docker em seu registro.
```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin (...)
```
### 6 - Crie sua imagem do Docker usando o comando a seguir.
```
docker build -t my-app-ecs:v1 .
```
### 7 - Depois que a compilação for concluída, marque sua imagem para que você possa enviar a imagem para este repositório:
```
docker tag my-app-ecs:v1 my-account.dkr.ecr.us-east-1.amazonaws.com/my-app-ecs:v1
```
### 8 - Execute o seguinte comando para enviar esta imagem para seu repositório recém-criado da AWS:
```
docker push my-account.dkr.ecr.us-east-1.amazonaws.com/my-app-ecs:v1
```
### 9 - Crie um cluster ECS do tipo "Fargate"...

### 10 - Crie uma task definition com a "URI Image" da sua imagem que foi enviada para o ECR, expondo na porta 80...

### 11 - Em seu cluster criado, adicione um "services" com launch type: Fargate, Application type: Service, em "Family" selecione a task definition criada...


# 🎉 Congratulations, you have deployed your first application using AWS ECS 🐋
