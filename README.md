#  ✅ Criar máquinas Virtuais em Clusters pelo Docker
#### Acessar as maquinas pelo Vagrant
    vagrant ssh node1
    sudo su
    ip a
    docker swarm init --advertise-addr 10.0.0.180
#### Acessar as outras maquinas virtuais e colar
    vagrant ssh node1
    sudo su
    docker swarm join --token SWMTKN-1-laksjlkajfhoqiuwehr09687alakjlksjfak-1lkj12kjh4j1ll1jklkj1h1l141883 10.0.0.180:2377
#### Visualizar os Clusters
      docker node ls
#### Destruir VMs
    vagrant destroy
## 🆑 Serviços em um Cluster
    docker service ls
    docker service create -name web-server --replicas 15 -p 80:80 httpd
    docker service ps web-server
#### Retirar os containers do node1 e deixar somente para genrência
    docker node update --availability drain node1
    docker service rm web-server // Matar todo o serviço criado
---
⌨️
✅
🆑
❗️
🔴
☑️
🔘
