# Rsh

The remote shell (rsh) is a command line computer program that can execute shell commands as another user, and on another computer across a computer network.

## Instalação

Toda a instalação é feita como root

### Debian

Instale o pacote rsh-server com o comando:

 `apt-get install rsh-server`

Instale o pacote xinetd com o comando:

 `apt-get install xinetd`

### CentOS

Instale o rsh-server com o comando:

 `yum -y install rsh-server`

## Configuração

Verifique se os arquivos rexec, rsh e rlogin existem na pasta /etc/xinetd.d/

Se não existirem copie o arquivo echo para rexec, rsh e rlogin com os comandos:

 ```
cp echo rexec
cp echo rsh
cp echo rlogin
```

Edite os arquivos rexec, rsh e rlogin

Se foram copiados do echo

Altere de:

 `service echo`

Para:

 `service exec (rexec), shell (rsh) e login (rlogin)`

Obs dentro do () é apenas o nome do arquivo, não incluir.

E sendo copiados ou já existindo

Altere de:

 `disable         = yes`

Para:

 `disable         = no`

Repita o processo para cada arquivo, sempre salvando e saindo

Edite o arquivo /etc/securetty

Adicione as linhas abaixo no final do arquivo

 ```
rsh
rexec
rlogin
```

Salve o arquivo e saia

Crie o arquivo .rhosts dentro do /root

E coloque o seguinte conteúdo

 `IP da máquina que irá usar`

**Obs:** Se não for usar como root que pode ser perigoso, siga os passos abaixo:

Crie o mesmo nome de usuário da máquina que vai acessar com o comando:

 `adduser usuario`

Mova o .rhosts do /root para a pasta /home/usuario com o comando:

 `mv /root/.rhosts /home/usuario`

Reinicie o serviço xinetd com o comando:

 `service xinetd restart`

## Testes

Testes: Da máquina que quer rodar comandos remotos no server dê o comando:

 `rsh ip_do_server comando`