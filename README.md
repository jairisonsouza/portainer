# Portainer - Gerenciamento de Containers Simplificado

Portainer é uma interface gráfica leve e fácil de usar para gerenciar ambientes de contêineres. Ele suporta plataformas como Docker, Docker Swarm, Kubernetes e Azure Container Instances, facilitando a administração e monitoramento dos serviços.

## Recursos principais
- **Interface web intuitiva** para gerenciamento de contêineres.
- **Compatibilidade com múltiplos ambientes** (Docker, Swarm, Kubernetes).
- **Gerenciamento simplificado de volumes, redes e stacks.**
- **Controle de acesso baseado em usuários e equipes.**
- **Implementação rápida e fácil.**

# AMBIENTE LOCAL:
## Pré requisitos:

* Docker
```
sudo apt install docker.io
```
* Docker-Compose
```
sudo apt install docker-compose
```

## Clone do Projeto:
```
git clone https://github.com/jairisonsouza/portainer.git
```

## Executando
Dentro da pasta do projeto, execute:
```
docker-compose up -d
```

Isso pode demorar um pouco, aguarde.

# AMBIENTE DE PRODUÇÂO:
## Pré requisitos:

* Docker
```
sudo apt install docker.io
```
* Docker-Swarm
```
docker swarm init
```

## Clone do Projeto:
```
git clone https://github.com/jairisonsouza/portainer.git
```

## Preparando ambiente:

Crie uma rede para o Portainer:

```
docker network create --driver overlay portainer-net --attachable
```

* Substitua o domínio "seudominio.com.br" no arquivo `docker-compose-swarm.yml` (linha 12), dentro da pasta `docker`:

## Executando:
Dentro da pasta do projeto, execute:
```
docker stack deploy -c docker/docker-compose-swarm.yml portainer
```

Isso pode demorar um pouco, aguarde.

## Acesso:

Para acessar o Portainer acesse o endereço: https://portainer.seudominio.com.br para realizar a configuração inicial.

Pronto, o Portainer foi configurado.
