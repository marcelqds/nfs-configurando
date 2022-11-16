# nfs-configurando (Debian / Ubuntu)


## Instalando e configurando o Server
Ip do servidor: 192.168.1.254

Primeiro iremos instalar o `nfs-kernel-server` na máquina que será efetuado o compartilhamento
```sh
sudo apt-get install nfs-kernel-server
```

Crie a pasta que será compartilhada, no nosso caso iremos compartilhar a pasta `dados` no diretório `/opt`
```sh
sudo mkdir `/opt/dados`
```

Criando compartilhamento no arquivo `/etc/exports`, abra o arquivo e informe o ip ou rede que terá acesso ao compartilhamento
- Compartilhando para rede `192.168.1.0/24`
```sh
/opt/dados 192.168.1.0/24(rw,sync,no_root_squash,no_subtree_check)
```
- Compartilhando para um ip específico, nesse caso para `192.168.1.100`
```sh
 /opt/dados 192.168.1.100(rw,sync,no_squash, no_subtree_check)
```

Após editar e salvar o arquivos `etc/exports`, disponibilize os compartilhamentos criados
```sh
sudo exportsfs -ar
```


## Instalando e configurando o Cliente
Ip do cliente: 192.168.1.100

Efetuando a instalação
```sh
sudo apt-get install nfs-common
```

Criando diretório onde será feito a montagem do compartilhamento.
```sh
sudo mkdir /opt/dados
```

```sh
mount -t nfs4 192.168.1.254:/opt/dados /opt/dados
```

