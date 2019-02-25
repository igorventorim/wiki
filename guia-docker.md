<!-- TITLE: Guia Docker -->
<!-- SUBTITLE: Um guia rápido de comandos docker -->
	
** [ INSTALAÇÃO DOCKER ] **

Ubuntu:

#### 	DOCUMENTATION https://docs.docker.com/install/

* 	 INSTALANDO O DOCKER
	`curl -fsSL https://get.docker.com/ | sh		`


* CentOS:

	
```sh
#Uninstall old versions: 
	sudo yum remove docker \
	                  docker-client \
	                  docker-client-latest \
	                  docker-common \
	                  docker-latest \
	                  docker-latest-logrotate \
	                  docker-logrotate \
	                  docker-selinux \
	                  docker-engine-selinux \
	                  docker-engin
```


	#Install repositories
	sudo yum install -y yum-utils \
	  device-mapper-persistent-data \
	  lvm2

	sudo yum-config-manager \
	    --add-repo \
	    https://download.docker.com/linux/centos/docker-ce.repo

    #Inicializando o docker
	sudo systemctl start docker

	#Install Docker-ce
	sudo yum install docker-ce

	#Start Docker
	sudo systemctl start docker

	#Test
	sudo docker run hello-world

##  [COMANDOS BÁSICOS DOCKER ]

* docker run hello-world						#EXECUTA O PRIMEIRO CONTAINER DOCKER PARA TESTAR SE O DOCKER FOI INSTALADO CORRETAMENTE.

* docker images								#EXIBI AS IMAGENS DOCKER BAIXADAS NO PROJETO.

* docker ps									#EXIBI OS CONTAINERS EM EXECUÇÃO.

* docker ps -a 								#EXIBI TODOS OS CONTAINERS.

* docker create <image>						#CRIA O CONTAINER MAS NÃO O EXECUTA.

* docker run -it ubuntu /bin/bash				# -it: Interative Terminal   - ubuntu: Distribuição   - /bin/bash: COMANDO TERMINAL

* docker attach <CONTAINER_ID>				#ENTRA NO TERMINAL INTERATIVO DE UM CONTAINER EM EXECUÇÃO
* 
* docker exec -ti <CONTAINER_ID> bash         #ENTRA NO TERMINAL INTERATIVO DE UM CONTAINER EM EXECUÇÃO

* docker start <CONTAINER_ID>					#INICIALIZA O CONTAINER

* docker stop <CONTAINER_ID>					#PARA O CONTAINER

* docker pause <CONTAINER_ID>					#PAUSA O CONTAINER

* docker unpause <CONTAINER_ID>				#DESPAUSA O CONTAINER

* docker stats <CONTAINER_ID>					#EXIBE OS RECURSOS CONSUMIDOS PELO CONTAINER

* docker top <CONTAINER_ID>					#EXIBE OS PROCESSOS SENDO EXECUTADOS NO CONTAINER

* docker logs <CONTAINER_ID>					#EXIBE OS LOGS DE TUDO QUE FOI EXECUTADO NO CONTAINER

* docker logs -t <CONTAINER_ID>				#LOG INTERATIVO DO CONTAINER

* docker rm <CONTAINER_ID>					#REMOVE SOMENTE O CONTAINER SE ESTIVER DESATIVADO

* docker rm -f <CONTAINER_ID>					#REMOVE O CONTAINER ATÉ MESMO ATIVADO

* docker rmi -f <IMAGE_ID>					#REMOVE UMA IMAGEM DA MÁQUINA

* docker exec <CONTAINER_ID> <COMMAND>		#EXECUTA O COMANDO DENTRO DO CONTAINER

* docker run <parammeters> <image>:<version> <command>
	**PARAMMETERS:**
	* -it:							#Terminal interativo
	* -d:								#Execução em background
	* --name <name>:					#Determina um nome para o container
	* --memory|-m <value>m			#Determina o limite de memória do container
	* --cpu-shares <value>			#Determina o limite de cpu do container
	* -v <volume_name>				#Cria um volume que será compartilhado entre o host e o container
	* -v <pathHost>:/<volume_name>	#Faz o link do volume no container com um repositório no host
	* -e VARIABLE=VALUE				#Cria variável de ambiente
	* --volumes-from <CONTAINER_ID>	#Importa o volume de um determinado container
	* -p HOST_PORT:CONTAINER_PORT		#Seta a porta de comunicação entre o container e o host
	* --restart=always				#Container sempre rebootavel


## [COMANDOS NO CONTAINER] 

* CTRL + P + Q: Sai do container sem finalizar.

* CTRL + D: Finaliza o container.

##  [COMANDOS INTERMEDIÁRIOS DOCKER ] 

* docker inspect <CONTAINER_ID>							#EXIBI TODAS AS INFORMAÇÕES REFERENTE AO CONTAINER

* docker inspect <CONTAINER_ID> | grep -i mem				#INSPENCIONA A QUANTIDADE DE MEMÓRIA ALOCADA AO CONTAINER
			"Memory": 0		=> 0 SIGNIFICA VALOR DE MEMÓRIA INDEFINIDO.

* docker inspect <CONTAINER_ID> | grep -i cpu				#INSPECIONA QUANTIDADE DE CPU ALOCADA

* docker inspect -f {{.Mounts}} <CONTAINER_ID>			#INSPECIONA O VOLUME DO CONTAINER, EXIBINDO O SEU PATH NO HOST

* docker update -m <Value>m <CONTAINER_ID>				#ATUALIZA O LIMITE DE MEMÓRIA DO CONTAINER

* docker update --cpu-shares <Value> <CONTAINER_ID>		#ATUALIZA O LIMITE DE CPU DO CONTAINER

* docker build -t <image name:vesion> <DOCKER_FILE_PATH>	#CONSTROI A IMAGEM


##  [EXEMPLOS]
* docker run -it --memory 256m --cpu-shares 512 --name teste ubuntu	#CRIA UM CONTAINER COM TERMINAL INTERATIVO MEMÓRIA LIMITADA A 256MiB e CPU também limitado, tendo como nome teste.


## [DOCKERFILE]

>  Dockerfile é semelhante a um makefile. A partir de um Dockerfile você cria uma imagem.

* FROM <ubuntu>						    => DETERMINA A IMAGEM BASE DO CONTAINER 

* MAINTAINER <IGOR VENTORIM>				=> RESPONSÁVEL PELO DOCKERFILE

* RUN <apt-get update && apt-get install apache2> 		=> UTILIZADO PARA INSTALAÇÃO DE PACOTES/ QUANTO MENOS RUN MELHOR POR CAUSA QUE CRIA MENOS CAMADAS - CONCATENE COMANDOS AO MÁXIMO.

* ADD opa.txt /diretorio/					=> COPIA QUALQUER ARQUIVO DO HOST PARA O CONTAINER

* CMD ["sh", "-c", "echo", "$HOME"]			=> CMD é um parâmetro do entrypoint

* LABEL Description="Lorem ipsum"				=> Adicionar meta dado ao container, como nome do fabricante e etc...

* COPY opa.txt /diretorio/				=> COPIA ALGUNS TIPOS DE ARQUIVOS DO HOST PARA O CONTAINER

* ENTRYPOINT ["/usr/bin/apache2ctl", "-D", "FOREGROUND"]	=> PERMITI QUE UM PROCESSO SEJA O PRINCIPAL PROCESSO DO CONTAINER, CASO ELE MORRA O CONTAINER MORRE.

* ENV meunome="Igor Ventorim"				=> CONFIGURE VARIÁVEIS DE AMBIENTE E ENVIA PARA DENTRO DO CONTAINER

* EXPOSE 80						=> EXPÕE A PORTA QUE SERÁ UTILIZADA PELO CONTAINER

* USER username						=> DEFINI QUAL O USUÁRIO DO CONTAINER

* WORKDIR	/rootpath					=> DEFINI O DIRETÓRIO RAIZ DO CONTAINER

* VOLUME	/diretorio					=> CRIA O VOLUME DO CONTAINER

* ONBUILD								=> DEFINI ALGUMAS INSTRUÇÕES A SEREM EXECUTADAS QUANDO UMA AÇÃO FOR REALIZADA



## [DOCKER HUB]

> Docker Hub é semelhante ao github, no entanto ele guarda imagens de containers em vez de código fonte. SITE: https://hub.docker.com/

* docker inspect <IMAGE_NAME>:<VERSION>			#INSPECIONA A IMAGEM

* docker history <IMAGE_NAME>:<VERSION> 			#EXIBI O HISTÓRICO DE CAMADAS

* docker tag <IMAGE_ID> <USERNAME>/<IMAGE_NAME>	#RENOMEIA UMA IMAGEM. IMAGEM PADRÃO DOCKERHUB

* docker login									#REALIZA O LOGIN NO DOCKER HUB

* docker push <IMAGE_ID>							#REALIZA O UPLOAD DA IMAGEM PARA O DOCKERHUB

* docker pull	<USERNAME>/<IMAGE_NAME>				#REALIZA O DOWNLOAD DA IMAGEM

* docker search <IMAGE>							#BUSCA IMAGENS NO DOCKER HUB


## [ NETWORK ] 

* docker run <parammeters> <image>:<version> <command>
**PARAMMETERS:**
	*--dns <X.X.X.X>								#SETANDO DNS DO CONTAINER
	*--hostname <name>							#NOME DO CONTAINER
	*--link <CONTAINER_ID>						#LINKA UM CONTAINER COM O OUTRO
	*--expose <PORT>								#EXPÕE A PORTA DO CONTAINER
	*--publish <PORT_HOST>:<PORT_CONTAINER>		#REALIZA O BIND DA PORTA DO HOST COM A DO CONTAINER
	*--mac-address <XX:XX:XX:XX:XX:XX>			#SETA O ENDEREÇO MAC DO CONTAINER
	*--net=host/bridge							#SETA AS CONFIGURAÇÕES DE REDES BASEADAS NO HOST


## [ DOCKER MACHINE ]

> ESTUDAR MAIS SOBRE DOCKER MACHINE https://docs.docker.com/machine/install-machine/

### Instalação para o docker machine Linux:
1. wget https://github.com/docker/machine/releases/download/v0.14.0/docker-machine-`uname -s`-`uname -m`
2. mv docker-machine-Linux-x86_64 /usr/local/bin/
3. chmod +x /usr/local/bin/docker-machine-Linux-x86_64
4. docker-machine-Linux-x86_64 --version

* docker-machine-Linux-x86_64 create --driver virtualbox <name>		

* docker-machine-Linux-x86_64 env <name>								

* docker-machine-Linux-x86_64 ssh <name>								

* docker-machine-Linux-x86_64 ip <name>								

* docker-machine-Linux-x86_64 stop <name>								

* docker-machine-Linux-x86_64 start <name>							

* docker-machine-Linux-x86_64 ls 										

* docker-machine-Linux-x86_64 rm 										

## [ DOCKER COMPOSE ] 

### Install docker-compose:
1. sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose

2. sudo chmod +x /usr/local/bin/docker-compose

3. docker-compose --version

* build = Indica o caminho do seu Dockerfile
	* build .

* command = Executa um comando
	*command bundle exec thin -p 3000

*container_name = Nome para container
	*container_name: my-web-container

*dns = Indica o dns server
	*dns: 8.8.8.8

*dns_search = Especifica um search domain
	*dns_search: example.com

*dockerfile = Especifica um Dockerfile alternativo
	*dockerfile: Dockerfile-alternate

*env_file = Especifica um arquivo com variáveis de ambiente
	*env_file: .env

*environment = Adiciona variáveis de ambiente
	*environment:
		*RACK_ENV: developmnet

*expose = Expõe a porta do container
	*expose :
		*- "3000"
		*- "8000"

*external_links = "Linka" containers que não estão especificados no docker-compose atual
	*external_links:
		*- redis_1
		*- project_db_1:mysql

*extra_hosts = Adiciona um entrada no /etc/hosts do container
		*- "somehost:162.242.195.82"
		*- "otherhost:50.31.209.229"

*image = Indica uma imagem
	*image: ubuntu:14.04

*labels = Adiciona metadata ao container
	*labels:
		*com.example.description: "Accounting webapp"
		*com.example.department: "Finance"

*links = Linka containers dentro do mesmo docker-compose
	*links:
		*- db
		*- db:database

*log_driver = Indica o formato do log a ser gerado, por ex: syslog, json-file, etc
	*log_driver: syslog
	ou
	*logging:
		*driver: syslog

*log_opt = Indica onde mandar os logs, pode ser local ou em um syslog remoto
	*log_opt:
		*syslog-address: "tcp://192.168.0.42:123"
		ou
	*logging:
		*driver: syslog
		*options:
			*syslog-address: "tcp://192.168.0.42:123"

*net = Modo de uso da rede
	*net: "bridge"
	*net: "host"

*ports = Expõe as portas do container e do host
	*ports:
		*- "3000"
		*- "8000:8000"

*volumes, volume_driver = Monta volumes no container
	*volumes:
		* Just specify a path and let the Engine create a volume
		*- /var/lib/mysql

	* Specify an absolute path mapping
		*- /opt/data:/var/lib/mysql

	* Path on the host, relative to the Compose file
		*- ./cache:/tmp/cache

*volumes_from = Monta volumes através de outro container
	*volumes_from:
		*- service_name
		*- service_name:ro

## [ DOCKER MODE SWARM ] 

