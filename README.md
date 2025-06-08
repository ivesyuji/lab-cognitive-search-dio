# Desvendando a Busca Cognitiva no Azure

Este espaço foi criado para documentar minha jornada prática e o aprendizado adquirido no desafio de aprofundar o uso do **Azure AI Search**. Aqui, você encontrará resumos, anotações e insights sobre como a Inteligência Artificial pode ser aplicada na **indexação, busca e extração de conhecimento de grandes volumes de dados**.

O objetivo principal deste laboratório foi desenvolver habilidades práticas na criação de soluções de busca inteligentes e na integração de capacidades de IA em dados. Este `README.md` serve como um guia detalhado, registrando as etapas realizadas e as conclusões obtidas, funcionando como um material de apoio valioso para estudos futuros e implementações.

## **Passo 01: Criação dos Recursos no Azure**

Para iniciar, precisamos provisionar os serviços fundamentais no Azure que darão suporte à nossa solução de busca e análise.

1. Acesse o **Portal do Azure** em [https://portal.azure.com/](https://portal.azure.com/) e faça login com sua conta Microsoft.
2. No menu superior esquerdo (as três barras), navegue até **"IA + Machine Learning"** e, em seguida, crie os três recursos a seguir, respectivamente: **Azure AI Search**, **Serviços de IA do Azure** e **Conta de Armazenamento**.

    > **Observação:** seus recursos de pesquisa do Azure AI e serviços do Azure AI devem estar no mesmo local!
### Azure AI Search

Este serviço será a base para sua capacidade de pesquisa e indexação de documentos.

![[Pasted image 20250608194730.png]]

**Configurações:**

- **Assinatura:** Selecione sua assinatura do Azure.
- **Grupo de Recursos:** Selecione um grupo de recursos existente ou crie um novo com um nome exclusivo.
- **Nome do Serviço:** Defina um nome exclusivo para seu serviço de pesquisa.
- **Localização:** Escolha qualquer região disponível. Se optar por "East US", utilize "East US 2" para maior compatibilidade.
- **Nível de Preço:** Selecione **Básico**.

Após preencher, clique em **"Revisar + criar"** e, após a validação bem-sucedida, selecione **"Criar"**.
### Serviços de IA do Azure

Este recurso fornecerá as capacidades de inteligência artificial, como análise de sentimento e extração de frases-chave, que serão integradas ao seu índice de pesquisa.

![[Pasted image 20250608194947.png]]

**Configurações:**

- **Assinatura:** Selecione sua assinatura do Azure.
- **Grupo de Recursos:** Utilize **o mesmo grupo de recursos** do seu recurso do Azure AI Search.
- **Região:** Selecione **o mesmo local** do seu recurso do Azure AI Search.
- **Nome:** Forneça um nome exclusivo para seu recurso.
- **Nível de Preço:** Escolha **Standard S0**.

Clique em **"Revisar + criar"** e, após a validação bem-sucedida, selecione **"Criar"**.
### Conta de armazenamento

A conta de armazenamento será usada para hospedar os documentos que você deseja indexar e pesquisar.

![[Pasted image 20250608194804.png]]

**Configurações:**

- **Assinatura:** Selecione sua assinatura do Azure.
- **Grupo de Recursos:** Utilize **o mesmo grupo de recursos** dos seus recursos do Azure AI Search e Serviços de IA do Azure.
- **Nome da Conta de Armazenamento:** Crie um nome exclusivo para sua conta de armazenamento.
- **Localização:** Escolha qualquer localização disponível (idealmente a mesma dos outros recursos).
- **Desempenho:** Selecione **Padrão**.
- **Redundância:** Escolha **Armazenamento redundante localmente (LRS)**.

Clique em **"Revisar"** e depois em **"Criar"**. Aguarde a conclusão da implantação e, em seguida, acesse o recurso implantado.

- No painel de menu à esquerda da sua conta de Armazenamento do Azure, selecione **"Configuração"** (dentro de **"Configurações"**).
- Altere a configuração **"Permitir acesso anônimo do Blob"** para **"Habilitado"** e clique em **"Salvar"**. Isso permitirá que o serviço de pesquisa acesse os documentos
## Passo 02: Upload dos Documentos para a Conta de Armazenamento

Agora que sua conta de armazenamento está pronta, vamos carregar os documentos que serão indexados.

1. Na sua conta de Armazenamento do Azure, no painel de menu à esquerda, selecione **"Contêineres"**.
![[Pasted image 20250608195517.png]]
    
2. Crie um novo contêiner com as seguintes configurações e clique em **"Criar"**:
    
    - **Nome:** `coffee-reviews`
    - **Nível de Acesso Público:** `Contêiner` (permite acesso de leitura anônimo para contêineres e blobs).
    - **Avançado:** Deixe as configurações padrão.
3. Em uma nova aba do navegador, baixe as [avaliações de café compactadas](https://aka.ms/mslearn-coffee-reviews) e extraia os arquivos para uma pasta (ex: `coffee-reviews`).
    
4. No portal do Azure, selecione o contêiner recém-criado `coffee-reviews`. Dentro do contêiner, clique em **"Upload"**.

![[Pasted image 20250608195732.png]]
    
5. No painel **"Carregar blob"**, clique em **"Selecionar um arquivo"**.

![[Pasted image 20250608195748.png]]
    
6. Na janela do explorador de arquivos, **selecione todos os arquivos** na pasta que você extraiu as avaliações de café, clique em **"Abrir"** e, em seguida, selecione **"Upload"**.
    
7. Após a conclusão do upload, você pode fechar o painel **"Upload de blobs"**. Seus documentos agora estão no contêiner de armazenamento `coffee-reviews`, prontos para serem indexados.

## Consultar o índice

Use o Explorador de Pesquisa para escrever e testar consultas. O Explorador de Pesquisa é uma ferramenta integrada ao portal do Azure que oferece uma maneira fácil de validar a qualidade do seu índice de pesquisa. Você pode usar o Explorador de Pesquisa para escrever consultas e revisar resultados em JSON.

1. Na página _Visão geral_ do serviço de pesquisa , selecione **Explorador de pesquisa** na parte superior da tela.

![[Pasted image 20250608195846.png]]

Observe que o índice selecionado é o _índice de café_ que você criou. Abaixo do índice selecionado, altere a _visualização_ para **JSON** .

![[Pasted image 20250608195902.png]]

Com isso, podemos **filtrar** os documentos e executar diferentes tipos de consultas para extrair informações específicas do seu índice.

## Conclusão:

Este laboratório foi fundamental para entender como construir uma **solução de busca inteligente** do zero no Azure. Aprendi na prática a:

- **Provisionar e configurar novos recursos** como **Azure AI Search**, **Serviços de IA do Azure** e **Contas de Armazenamento**, compreendendo suas interconexões e importância.
- **Preparar e carregar dados** para indexação, tornando-os acessíveis para processamento de IA.
- **Utilizar o Explorador de Pesquisa** para testar e validar o índice, aplicando consultas para **filtrar e extrair insights** de documentos.

Essa experiência me permitiu ver como a **Inteligência Artificial** pode transformar grandes volumes de dados brutos em **informações valiosas**, abrindo portas para a mineração de conhecimento e a criação de sistemas de busca poderosos.
