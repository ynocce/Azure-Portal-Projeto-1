# Como criar uma VM com ISS e Deployment Groups.

Esse documentação tem como objetivo orientar como criar uma VM com ISS e Deployment Group para ser usado em uma release no Azure DevOps de uma aplicação .NET Core.

Vamos usar:

- Azure Portal.
- Azure DevOps.

- Criando uma VM com Window Server 2016 no Azure Portal.
    
    1 - Acesse o Azure Portal: [https://portal.azure.com/](https://portal.azure.com/) e procure o serviço de Maquina Virtual e clique em criar
    
    2 - Iremos criar uma VM com Windows server 2016.
    
    - Crie um Grupo de Recurso.
    - Escolha o nome da VM e a região.
    - Não iremos precisar de availability zones.
    - segurança vamos deixar como padrão.
    - Selecione a imagem Windows Server 2016 x64 Gen2
    - Escolha a VM que você deseja utilizar.
        
        No meu caso irei utilizar a mais barata por hora.
        
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled.png)
    
    3 - Crie um usuário para acessar a VM e Libere as portas conforme a imagem abaixo:
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%201.png)
    
    4 - Agora clique em revisar e Criar.
    
    Nota: Sobre o armazenamento e a rede, fica ao seu critério. 
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%202.png)
    
    5 - Agora acesse a tela da VM criada para configurarmos o endereço DNS.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%203.png)
    
    6 - Nessa tela ira mostrar nosso IP e também se ele está estático ou dinâmico.
    
    Conforme imagem abaixo, crie seu endereço DNS e salve em um bloco de notas.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%204.png)
    
    7 - Agora acesse sua maquina virtual usando o DNS que você criou.
    
    Aperte Win + R e coloque: “ mstsc “ e aperte enter.
    
    Quando abrir o RDP, coloque o endereço DNS que criou.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%205.png)
    
- Configurando o ISS no Windows Server 2016.
    
    1 - Instale o ISS no servidor, clicando em Manage → Add Roles and Features.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%206.png)
    
    2 - Agora clique em Next até chegar em Server roles.
    
    Before You Begin → Installation Type → Server Selection → Server Roles e marque Web Server (IIS).
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%207.png)
    
    3- Clique em **Add Features** e next.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%208.png)
    
    4 - Em Features marque **IIS Hostable Web Core** e Next.
    
    Nas próximas telas, clique em Next até chegar na parte de **Install** e aguarde.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%209.png)
    
    5 - Verificando seu o ISS foi instalado, acesse Tools e Clique em ISS. Pronto o ISS foi instalado
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2010.png)
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2011.png)
    
    6 - Instale o .NET Core na VM.
    
    Link: [https://dotnet.microsoft.com/pt-br/download/dotnet/8.0](https://dotnet.microsoft.com/pt-br/download/dotnet/8.0)
    
    Apenas execute o arquivo e clique em next e aguarde.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2012.png)
    
    7 - Acessando nosso localhost na VM.
    
    Abra o navegador e pesquise: localhost
    
    Você também pode visualizar pelo nosso endereço DNS da VM.
    
    Nota: A porta 80 - HTTP tem que está habilitada na VM.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2013.png)
    
    8 - Acesse a VM e abre o ISS. 
    
    Apague o Default Web Site.
    Apague o Application Pools.
    
    Reset o ISS, pelo powershell: `IISRESET`
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2014.png)
    
- Instalando Deployment Group na VM.
    
    1 - Acesse seu Azure DevOps → Pipelines → Deployment Groups
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2015.png)
    
    2 - Coloque um nome no seu Deployment Group e marque para usar um personal Access Token.
    
    Copie o Script e cole no PowerShell na VM com o ISS.
    Nota: use o PowerShell como administrador. 
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2016.png)
    
    3 - Nesse caso não vamos querer tags, então coloque N. 
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2017.png)
    
    4 - Acesse o Azure DevOps → Pipelines → Deployment Groups. 
    
    Pronto está funcionando no DG e online, para realizarmos o Deploy.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2018.png)
    
- Configurando uma Release com o Deployment Group.
    
    1 - Acesse o Azure DevOps → Pipelines → Releases → Crie uma Nova release.
    
    Pesquise por ISS e procure a task IIS website deployment.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2019.png)
    
    2 - Selecione o artefato gerado por sua buid .NET e clique em ADD.
    
    Nota: Caso você não tenha uma Build .NET, acesse meu [**Github**](https://github.com/ynocce/Az-DevOps-Projeto-1) para aprender como criar. 
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2020.png)
    
    3 - Clique no Stage → Deploy → Coloque o nome no seu Website
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2021.png)
    
    4 - Clique em ISS deployment e selecione o deployment Group que criamos: 
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2022.png)
    
    5 - Na task de ISS Web App Manage, configure conforme a imagem abaixo e clique em **salvar.**
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2023.png)
    
    6 - Clique em Create release → Marque o Stage de Deploy → Selecione a versão do Build. → Create → E faça o Deploy.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2024.png)
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2025.png)
    
    7 - Deploy realizado com sucesso, agora acesse o ISS na VM.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2026.png)
    
    8 - Em tools na VM acesse o ISS. Podemos verificar que foi feito o Deploy do nosso Web site na VM.
    
    ![Untitled](Como%20criar%20uma%20VM%20com%20ISS%20e%20Deployment%20Groups%2039dd055f53bc48bea4c95513e9cb1ec6/Untitled%2027.png)
    
    9 - Agora abra o endereço DNS da nossa VM no seu navegador. 
    
    Pronto, foi feito Deploy da sua aplicação utilizando o Deployment Group + ISS.
    
    Espero que tenha ajudado você com esse tutorial :-D.