# DOCUMENTAÇÃO SIMPLIFICADA GITFLOW

- Branch master - É a branch que contém código em nível de produção, ou seja, o código mais maduro existente na sua aplicação. Todo o código novo produzido eventualmente é juntado com a branch master, em algum momento do desenvolvimento;

- Branch develop - É a branch que contém código em nível preparatório para o próximo deploy. Ou seja, quando features são terminadas, elas são juntadas com a branch develop, testadas (em conjunto, no caso de mais de uma feature), e somente depois as atualizações da branch develop passam por mais um processo para então ser juntadas com a branch master;

- Branches feature/* - São branches no qual são desenvolvidos recursos novos para o projeto em questão. Essas branches tem por convenção nome começando com feature/ (exemplo: feature/new-layout) e são criadas a partir da branch develop (pois um recurso pode depender diretamente de outro recurso em algumas situações), e, ao final, são juntadas com a branch develop;

- Branches hotfix/* - São branches no qual são realizadas correções de bugs críticos encontrados em ambiente de produção, e que por isso são criadas a partir da branch master, e são juntadas diretamente com a branch master e com a branch develop (pois os próximos deploys também devem receber correções de bugs críticos, certo?). Por convenção, essas branches tem o nome começando com hotfix/ e terminando com o próximo sub-número de versão (exemplo: hotfix/2.31.1), normalmente seguindo as regras de algum padrão de versionamento;

- Branches release/* - São branches com um nível de confiança maior do que a branch develop, e que se encontram em nível de preparação para ser juntada com a branch master e com a branch develop (para caso tenha ocorrido alguma correção de bug na branch release/* em questão). Note que, nessas branches, bugs encontrados durante os testes das features que vão para produção podem ser corrigidos mais tranquilamente, antes de irem efetivamente para produção. Por convenção, essas branches tem o nome começando com release/ e terminando com o número da próxima versão do software (seguindo o exemplo do hotfix, dado acima, seria algo como release/2.32.0), normalmente seguindo as regras do versionamento semântico;

 O SEGUINTE WORKFLOW PERMITE MANTER OS BRANCHS DEVELOPER E MASTER SEMPRE ATUALIZADOS E ORGANIZADOS DE ACORDO COM A REALIZAÇÃO DE ALTERAÇÕES NO CÓDIGO.

 1 - git flow init (CONFIG DEFAULT): 
  * INICIA O GIT FLOW NO REPOSITÓRIO.

 2 - git flow feature start <NAME FEATURE>
  * CRIA UM BRANCH PARA TRABALHAR A NOVA FEATURE E MUDA PARA ELE.	

 3 - git status
  * (Permite conferir se você está no branch da feature)

 4 - git add ... git commit -m ...
   * ADICIONA OS ARQUIVOS A SEREM ENVIADOS E REALIZA O COMMIT. 

 5 - git flow feature finish <NAME FEATURE>
  * FINALIZA A FEATURE CRIADA REALIZANDO O MERGE AUTOMÁTICO E MUDANDO PARA O BRANCH DEVELOP. APÓS ISSO PODE SER REALIZADO O PUSH NO BRANCH DEVELOP PARA SUBIR A VERSÃO PARA O AMBIENTE DE DEV. 

 6 - git flow release start <0.1.0>
  * CRIA O BRANCH PARA SUBIR A NOVA RELEASE. VERSÃO DA RELEASE DEVERÁ SER BASEADA NO POM.XML

 7 - git add ... git commit -m ...
  * ADICIONA OS ARQUIVOS A SEREM ENVIADOS E REALIZA O COMMIT. 

 8 - git flow release finish <version release>
  * FINALIZA A RELEASE CRIADA REALIZANDO O MERGE AUTOMÁTICO E MUDANDO PARA O BRANCH MASTER. APÓS ISSO PODE SER REALIZADO O PUSH NO BRANCH MASTER PARA SUBIR A NOVA RELEASE.

 9 - git flow hotfix start <0.1.1>
  * EM CASO DE PROBLEMAS NA RELEASE EM QUESTÃO CRIA-SE UM HOTFIX COM O NÚMERO DA RELEASE ACRESCENTADO 0.0.1.

 10 - git add ... git commit -m ...
  * ADICIONA OS ARQUIVOS A SEREM ENVIADOS E REALIZA O COMMIT. 

 11 - git flow hotfix finish <0.1.1>
  * FINALIZA O HOTFIX CRIADO REALIZANDO O MERGE AUTOMÁTICA E JUNTA COM O BRANCH MASTER E DEVELOP. APÓS ISSO PODE SER REALIZADO O PUSH NO BRANCH MASTER PARA SUBIR A CORREÇÃO DO BUG.

