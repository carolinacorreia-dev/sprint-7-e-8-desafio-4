# sprint-7-e-8-desafio-4
Criar uma pipeline que faça o deploy do NGINX e que rode automaticamente após cada alteração

Objetivo

Esta documentação descreve o processo de criação de uma pipeline no GitLab que realiza automaticamente o deploy do NGINX após cada alteração no repositório.
Pré-requisitos

Antes de começar, certifique-se de ter o seguinte:

    Uma conta no GitLab.
    Um repositório GitLab configurado para o seu projeto.
  
Passos
1. Criar um Repositório no GitLab

1.1. Faça login na sua conta do GitLab.

1.2. No GitLab, clique em "New Project" para criar um novo repositório.

1.3. Preencha as informações do projeto, como nome, descrição e visibilidade, e clique em "Create Project".

2. Adicionar o Arquivo .gitlab-ci.yml

2.1. No diretório raiz do seu projeto, crie um arquivo chamado .gitlab-ci.yml.

2.2. Abra o arquivo .gitlab-ci.yml em um editor de texto e adicione o seguinte conteúdo:

stages:
  - deploy

before_script:
  - apt-get update -qy

deploy_nginx:
  stage: deploy
  script:
    - apt-get install -y nginx
    - systemctl start nginx

deploy:
  stage: deploy
  script:
    - echo "Deploying NGINX..."
  only:
    - main

3. Configurar Gatilho Automático

3.1. No arquivo .gitlab-ci.yml, o trecho only: - main garante que a pipeline seja executada apenas quando houver alterações no branch main. Ajuste conforme necessário para o nome do seu branch padrão.

4. Commit e Push

4.1. Adicione o arquivo .gitlab-ci.yml ao seu repositório:

bash

git add .gitlab-ci.yml

4.2. Faça um commit com uma mensagem descritiva:

bash

git commit -m "Adiciona configuração da pipeline para deploy do NGINX"

4.3. Faça push das alterações para o GitLab:

bash

git push origin main  # ou o nome do seu branch padrão

5. Verificar a Execução da Pipeline

5.1. No GitLab, vá até o seu projeto e clique na seção "CI / CD" no menu lateral.

5.2. Você verá a execução da sua pipeline. Se não for acionada automaticamente, você também pode acioná-la manualmente.

Conclusão

Com esses passos, você configurou uma pipeline no GitLab que realiza automaticamente o deploy do NGINX após cada alteração no repositório. Lembre-se de ajustar as configurações conforme necessário para atender aos requisitos específicos do seu projeto.
