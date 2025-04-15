📬  # Automação de E-mails N8N 

🔍 ## Descrição do Projeto

Este fluxo de automação foi desenvolvido para o time financeiro, 
com o objetivo de automatizar o processo de recebimento de e-mails com anexos em formato CSV.

🛠️ A automação realiza os seguintes passos:

1. Recebe e-mails com arquivos CSV como anexos.
2. Baixa e salva esses arquivos em uma pasta específica no Google Drive.
3. Envia um e-mail de confirmação para o remetente, informando que o arquivo foi recebido com sucesso.
4. Marca o e-mail como lido para evitar duplicação no fluxo.

## Estrutura do Fluxo

🛠️ O fluxo de automação é composto pelas seguintes etapas:

1. **Gatilho de e-mail (Gmail Trigger)**: Monitora a caixa de entrada para novos e-mails a cada minuto.
2. **Filtragem de e-mails (Filter Node)**: Verifica se o e-mail contém um anexo.
3. **Baixar o anexo (Gmail Get: Message)**: Baixa o anexo CSV do e-mail.
4. **Salvar o arquivo CSV (Google Drive)**: Salva o arquivo CSV em uma pasta específica no Google Drive.
5. **Enviar e-mail de confirmação (Gmail Send: Message)**: Envia um e-mail ao remetente confirmando o recebimento do arquivo.
6. **Marcar o e-mail como lido (Gmail Mark as Read)**: Marca o e-mail como lido para evitar que o fluxo seja repetido.

## Passo a Passo para Configuração

📬  ### Passo 1: Configurar o Gatilho de E-mail

1. **Gmail Trigger**: Adicione um "Gmail Trigger" no n8n e configure-o no modo "Every Minute" para verificar novos e-mails a cada minuto.
   - **Evento**: `Message Received`
   - **Opções**: 
     - `Unread emails only` para filtrar e-mails não lidos.
     - Habilite o download de anexos (prefixo "attachment").

📁 ### Passo 2: Filtrar e Extrair o Arquivo CSV

1. **Filter Node**: Adicione um nó de filtro para verificar se o e-mail contém um anexo. Utilize a condição `attachment` para identificar os e-mails com anexo.

📁 ### Passo 3: Baixar o Anexo

1. **Gmail Get: Message**: Adicione um nó "Gmail Get: Message" para obter o conteúdo do e-mail e baixar o anexo.
   - Conecte suas credenciais do Gmail.
   - Habilite o download dos anexos.
   - O arquivo será identificado pelo prefixo "attachment" e estará disponível para os próximos passos.

📁 ### Passo 4: Salvar o Arquivo CSV no Google Drive

1. **Google Drive**: Adicione um nó "Google Drive" para fazer o upload do arquivo CSV em uma pasta específica.
   - **Autenticação**: Autorize o n8n a acessar sua conta do Google Drive.
   - **Pasta de Destino**: Crie uma pasta chamada "Arquivos CSV" no Google Drive e configure o nó para fazer o upload do arquivo na pasta.

📬 ### Passo 5: Enviar o E-mail de Confirmação

1. **Gmail Send: Message**: Adicione um nó "Send Email" para enviar uma confirmação ao remetente.
   - **To**: Utilize a variável que identifica o e-mail do remetente.
   - **Subject**: Defina o mesmo assunto do e-mail original.
   - **Message**: Exemplo de mensagem: "Arquivo CSV recebido com sucesso!"

📬 ### Passo 6: Marcar o E-mail como Lido

1. **Gmail Mark as Read**: Adicione um nó "Mark as Read" para marcar o e-mail como lido após o processamento, evitando que ele passe novamente pelo fluxo.

🌐 ### Conectar os Nós

Conecte os nós na seguinte ordem:

```
Gmail Trigger → Filter → Gmail Get: Message → Google Drive → Gmail Send: Message → Gmail Mark as Read → Fim
```

🌐 ## Configuração das Credenciais IMAP do Gmail

Para configurar o n8n com o Gmail, siga as instruções abaixo:

1. Ative a verificação em duas etapas na sua conta do Gmail.
2. Gere uma senha de aplicativo e habilite a verificação em duas etapas.
3. Utilize as seguintes configurações no n8n:
   - **Host**: imap.gmail.com
   - **Porta**: 993 (SSL)
   - **Usuário**: [Seu endereço de e-mail do Gmail]
   - **Senha**: Senha do aplicativo gerada


👉 ## Links Úteis

- [Documentação do IMAP no n8n](https://docs.n8n.io/integrations/builtin/credentials/imap/gmail/)
- [Documentação do Google Drive no n8n](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googledrive/file-operations/)
- [Documentação de credenciais do Google OAuth](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-generic/)

👉 ## Considerações Finais

Este fluxo pode ser adaptado para outros tipos de e-mails ou anexos, e você pode expandir a automação com mais funcionalidades, como o envio de relatórios ou a execução de tarefas adicionais após o recebimento dos arquivos CSV.
