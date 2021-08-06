# securePipeline
Uma meneira de integrar mais segurança ao seu CI e seu código!

Você precisará:

-   1 Conta da AWS com usuário com direitos de administrador e com credencias de Git para o AWS CodeCommit;
-   Ter o Git instalado localmente na sua máquina; 
-   1 Conta já criada no Trend Micro Cloud One; 

Essa demo irá criar:

-   2 Templates no AWS CloudFormation;
-   1 Repositório no AWS CodePipeline;
-   1 Build/ Projeto de Compilação no AWS CodeBuild;
-   1 Pipeline no AWS CodePipeline;
-   2 Buckets no AWS S3;
-   1 Parâmetro no AWS Systems Manager
-   2 Roles no AWS IAM Role  

Como Usar:

1- Clone o Repositório para a sua máquina: https://github.com/SecurityForCloudBuilders/Protect-a-Vulnerable-WebApplication.git

2- Execute o template codecommit.repository.template.yaml na Console da AWS -> Cloud Formation

2.5- Espere até que essa Stack apareça como "CREATE_COMPLETE"

3- Vá até o serviço "CodeCommit", nele irá aparecer um novo repositório vazio chamado "MyVulnerableApp"

4- Nessa mesma tela, do lado direito do nome desse repo, clique no botão azul "HTTPS" que aparece abaixo da frase "Clonar URL"

5- Também Clone esse Repositório para a sua máquina. Copie todo o conteúdo do primeiro repo (Protect-a-Vulnerable-WebApplication) e cole nesse diretório/ repositório (MyVulnerableApp)

6- Faça o push para o AWS CodeCommit do repositório (MyVulnerableApp)

7- Agora, faça o deploy do template "main.pipeline.template.yaml". Para isso, vá até o serviço do "Cloud Formation"

8.5- Esse template precisa que você providencie 2 parâmetros. O primeiro é o seu Snyk Token (Consegue encontrar ele na console do Open Source Security) e o outro é o nome do seu repositório, que no nosso caso (e se você estiver seguindo ele) é MyVulnerableApp

7.5- Espere até que essa Stack apareça como "CREATE_COMPLETE"

8- Para ver o resultado do Scan, vá ate o serviço "CodePipeline", para isso, nessa mesma tela do Cloud Formation e no o template que acabou de ser criado, clique na aba "Saída" ou "Outputs", e clique no link que aparece ao lado do nome "SecurePipeline"

9- Você será redirecionado para o Pipeline criado que já está sendo executado. Na segunda etapa com o nome "Scan-The-Code-With-Snyk-CLI", clique em detalhes 

10- Você será redirecionado para o "CodeBuild" e diretamente na compilação onde acontece o escaneamento do código. Vá atá as últimas linhas do Log da Compilação.

11- Nessas últimas linhas verá que foi gerado um link "Explore this snapshot at https://app.snyk.io/org/mais-alguma-coisa-aqui", copie esse link e cole no seu navegador. 

12- O report com os findings estará todo detalhado nele. 