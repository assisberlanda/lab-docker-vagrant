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
#### Cria um servico de cluster com swarm de uma imagem Apache com 15 replicas
    docker service ls
    docker service create --name web-server --replicas 15 -p 80:80 httpd
    docker service ps web-server
#### Retirar os containers do node1 e deixar somente para genrência
    docker node update --availability drain node1
    docker service rm web-server // Matar todo o serviço criado
## 🔴 Consistencia de Dados
    docker volume create app
    cd var/lib/docker/volumes/app/_data/
    nano index.html
    cd ..
    docker service ps meu-app
#### Criando 15 replicas
    ocker service create -name meu-app --replicas 15 -dt -p 80:80 --mount type=volume,src=app,dst=/usr/local/apache2/htdocs/ httpd
### ⌨️ NFS
    apt-get install nfs-server -y
    cd var/lib/docker/volumes/app/_data/
    nano /etc/exports
    // no final do arquivo cole o caminho abaixo e salve
    // var/lib/docker/volumes/app/_data/ *(rw,sync,subtree_check)
    exportsfs -ar
    // Editar regras de segurança e liberar o firewall para NFS
#### Montar nas demais maquinas NFS
    apt-get install nfs-commom -y
    // Editar regras de segurança e liberar o firewall para UDPs
    showmount -e 172.31.0.185 // ip da primeira máquina
    exportsfs -ar // Repita export na primeira máquina
    mount 172.31.0.185/var/lib/docker/volumes/app/_data/ var/lib/docker/volumes/app/_data/
#### Ir nas outras máquinas e executar
    sudo su
    apt-get install nfs-commom -y
    mount 172.31.0.185/var/lib/docker/volumes/app/_data/ var/lib/docker/volumes/app/_data/
## 🔘 Load Balance
### ❗️Cria logs em PHP de uma aplicação para ver os acessos
#### Denilson Bonatti [Repositório](https://github.com/denilsonbonatti/docker-app-cluster)
#### Site de Teste de Load Balance [Teste](https://loader.io/)

