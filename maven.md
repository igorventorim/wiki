					*** ____ ESTUDOS MAVEN ____ ***

MAVEN é uma ferramenta para o processo de build em qualquer linguagem que utiliza a JVM.					

========================================> [ INSTALAÇÃO MAVEN ] <============================================

Ubuntu:
	apt-get update && apt-get install maven

	mvn -v

=========================================> [ GERENCIAMENTO MAVEN ] <==========================================

Build: 

Repositórios:

Dependências:

=========================================> [ COMANDOS BÁSICOS MAVEN ] <==========================================

# Exclui a pasta target do projeto
mvn clean

#Copia as depedências(JAR) para target/dependency [Evita eventuais problemas de ambiente]
mvn dependency:copy-dependencies

# Compila o projeto
mvn compile		

# Executa os testes do projeto
mvn test		

#Compila e empacota o projeto, e permite utilizá-lo como depedência em outros projetos localmente
mvn install

#Compila e empacota o projeto
mvn package		

# Boa prática utilizada para gerar o pacote de deploy do projeto
mvn clean install

# Limpa o projeto, copia as depedências e empacota o projeto(Executando todas as fases necessárias)
mvn clean dependency:copy-dependencies package

# Exibi os últimos comandos maven utilizados
history | grep mvn

# Criando projeto maven desktop java(jar)
mvn archetype:generate \
 -DgroupId=com.mycompany.app \
 -DartifactId=my-app \
 -DarchetypeArtifactId=maven-archetype-quickstart \
 -Dversion=1.0-SNAPSHOT 


#Criando projeto maven web
mvn archetype:generate \
 -DarchetypeGroupId=org.apache.maven.archetypes \
 -DarchetypeArtifactId=maven-archetype-webapp \
 -Dversion=1.0-SNAPSHOT \
 -DgroupId=com.erkobridee.exemplo.mvn \
 -DartifactId=ExemploMavenWeb

#Adaptando o projeto para o eclipse
mvn eclipse:eclipse 				

=========================================> [ POM.XML ] <==========================================

Project Object Model – se trata do ponto de partida para o maven executar seu lifecycle. Nada mais é do que um arquivo XML que descreve propriedades e características do projeto.

<dependency>
		<groupId> </groupId>
		<artifactId> </artifactId>
		<version> </version>
		<scope> </scope>
</dependency>

TAG:scope - 
	compile: escopo padrão do maven para o momento em que o código é compilado e vai junto com o artefato;
	provided: adicionado no momento da compilação, mas não vai junto com o artefato. Dessa forma você está dizendo que a dependência virá de maneira transitiva de alguma outra dependência;
	runtime: não inclui no artefato, pois estará disponível em tempo de execução;
	test: inclui apenas no escopo de testes;
	system: não inclui no artefato, pois estará disponível no ambiente;
	import: incluirá TODAS as dependências do ‘depencyManagement‘ que está definido no pom ‘parent’.