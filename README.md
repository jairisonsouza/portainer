# Portainer - Gerenciamento de Containers Simplificado

Portainer é uma interface gráfica leve e fácil de usar para gerenciar ambientes de contêineres. Ele suporta plataformas como Docker, Docker Swarm, Kubernetes e Azure Container Instances, facilitando a administração e monitoramento dos serviços.

## Recursos principais
- **Interface web intuitiva** para gerenciamento de contêineres.
- **Compatibilidade com múltiplos ambientes** (Docker, Swarm, Kubernetes).
- **Gerenciamento simplificado de volumes, redes e stacks.**
- **Controle de acesso baseado em usuários e equipes.**
- **Implementação rápida e fácil.**

## Clone do Projeto:

Para clonar os arquivos do Portainer para o servidor, execute o comando:
```
git clone https://github.com/jairisonsouza/portainer.git
```

## Instalação
Para rodar o Portainer em produção:

## Pré requisitos:

* Docker
```
sudo apt install docker.io -y
```
* Docker-compose
```
sudo apt install docker-compose -y
```
* Docker-Swarm
```
docker swarm init
```

## Preparando ambiente:

Crie uma rede para o Portainer:

```
docker network create --driver overlay portainer-net --attachable
```

Certifique-se que o domínio e as portas do portainer estão corretas no arquivo `docker-compose.yml`:
```
version: '3.9'

services:
  portainer:
    image: portainer/portainer-ce:latest
    deploy:
      replicas: 1
      restart_policy:
        condition: any
      labels:
        - "traefik.enable=true"
        - "traefik.http.routers.portainer.rule=Host(`portainer.seudominio.com`)" # Substitua pelo seu domínio
        - "traefik.http.routers.portainer.entrypoints=websecure"
        - "traefik.http.routers.portainer.tls.certresolver=myresolver"
        - "traefik.http.services.portainer.loadbalancer.server.port=9000"
    networks:
      - portainer-net
    ports:
      - 9443:9443 # use 9000 para HTTP
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro # Necessário para gerenciar o Docker host
      - portainer_data:/data

volumes:
  portainer_data:

networks:
  portainer-net:
    external: true

```

## Executando:

* Para fazer a instalação do Portainer, execute o comando dentro da pasta onde o Portainer foi clonado:
```
docker stack deploy -c docker-compose.yml portainer
```

Isso pode demorar um pouco, aguarde.

Para certificar que tudo está funcionando, execute o comando `docker stack ls` para visualizar as Stacks em execução. Caso necessário verifique os logs do serviço com `docker logs <ID_CONTEINER>`.

Caso necessário, altere o arquivo `docker-compose.yml` e execute novamente o comando `docker stack deploy -c docker-compose.yml portainer` para atualizar a aplicação.

## Acesso:

Para acessar o Portainer acesse o endereço: https://portainer.detran.ap.gov.br ou https://ip_do_host:9443 para realizar a configuração inicial.

Um usuário administrador deverá ser criado no primeiro acesso.

Pronto, o Portainer foi configurado.
