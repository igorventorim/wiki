					*** ____ ESTUDOS GITLAB ____ ***

========================================> [ INSTALAÇÃO GITLAB RUNNER ] <============================================

#Adicionando repositório oficial.
	# For Debian/Ubuntu/Mint
	curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh | sudo bash

	 # For RHEL/CentOS/Fedora
	curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.rpm.sh | sudo bash

#INSTALANDO GITLAB RUNNER
	# For Debian/Ubuntu/Mint
	sudo apt-get install gitlab-runner

	# For RHEL/CentOS/Fedora
	sudo yum install gitlab-runner

#REGISTRANDO GITLAB RUNNER
sudo gitlab-runner register

	Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com )
	https://git.ufes.br

	Please enter the gitlab-ci token for this runner
	(GET VALUE IN https://git.ufes.br/igor.ventorim/edital/settings/ci_cd >> RUNNERS)

	Please enter the gitlab-ci description for this runner
	(NAME RUNNER)

	Please enter the gitlab-ci tags for this runner (comma separated):
	(Tags de invocação Runner)

	Please enter the executor: ssh, docker+machine, docker-ssh+machine, kubernetes, docker, parallels, virtualbox, docker-ssh, shell:
	(Escolher executor Runner)


#REGISTRANDO GITLAB RUNNER COM APENAS UM COMANDO
sudo gitlab-runner register -n \
  --url https://git.ufes.br/ \
  --registration-token Vymr6w7QQ4xvfrFFheyr \
  --executor shell \
  --description "Docente Runner"



========================================> [ GITLAB CI ] <===========================================================

Necessário a criação do arquivo .gitlab-ci.yml na raiz do repositório para ativar o CI.

# Exemplo:

#variables:
#  MAVEN_CLI_OPTS: "-s .m2/settings.xml --batch-mode"
#  MAVEN_OPTS: "-Dmaven.repo.local=.m2/repository"
#  PASTA_CODIGOFONTE: "codigo/edital/"
#  CONTAINER_NAME: "$CI_REGISTRY_IMAGE:$CI_COMMIT_REF_SLUG"

stages:
    - build
    - container
    - deploy
    
build:
   stage: build
   image: maven:latest
   script:
     - mvn clean install
     - cp target/*.war .
     - mvn clean
   artifacts:
     paths:
       - ./*.war
     expire_in: 1 week 
   tags:
     - docker-edital
   only:
     - master
     - dev
     
deploy_dev:
   stage: deploy
   dependencies:
     - build
   script:
     - cp *.war /opt/webapps/devedital/
     - docker restart devedital_application
   tags:
     - devlattes2
   environment:
     name: desenvolvimento
     url: https://devedital.ufes.br
   only:
     - dev
     
deploy_master:
   stage: deploy
   dependencies:
     - build
   script:
     - cp *.war /opt/webapps/edital/
     - docker restart edital_application
   tags:
     - devlattes
   environment:
     name: producao
     url: https://edital.ufes.br
   when: manual
   only:
     - master