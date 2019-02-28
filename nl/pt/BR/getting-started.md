---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-05"

---
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:DomainName: data-hd-keyref="DomainName"}

# Introdução ao {{site.data.keyword.cloud_notm}} Mass Data Migration
{: # GettingStarted}

** Pré-requisitos **

Reúna essas informações antes de enviar uma solicitação ao Mass Data Migration e concluir a migração.

1. Configurações de rede para o dispositivo de armazenamento
   - Endereço IP estático
   - Máscara de rede para ativação da transferência de dados
2. Configurações de rede para computador remoto
   - Endereço IP estático
   - Máscara de rede
   - Gateway padrão para acessar a interface com o usuário
3. Destino de download do Cloud Object Storage <br/>

   Deve-se ter pelo menos uma conta do {{site.data.keyword.cos_full}} e um depósito na Região Cruzada Padrão dos EUA ou na Região Cruzada da UE para completar o formulário de solicitação. Se você ainda não tiver uma conta do {{site.data.keyword.cos_full_notm}}}, crie uma antes de solicitar o dispositivo Mass Data Migration. Consulte [Sobre o {{site.data.keyword.cos_full}}](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage){:new_window}.
   {:important}

## Criando uma Solicitação

1. Efetue login no [console do IBM Cloud](https://{DomainName}/){:new_window} e clique no ícone de menu na parte superior esquerda. Selecione **Infrastructure**.

   Como alternativa, é possível efetuar login no console do [{{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/){:new_window}.
2. Selecione **Armazenamento** > **Migração de dados** > **Mass Data Migration** na Barra de navegação para acessar a página de entrada do Mass Data Migration.
3. Clique em **Solicitar dispositivo** para abrir o formulário do pedido.
4. Preencha cada campo no formulário do pedido **Mass Data Migration**.
   - **Endereço de entrega**: esse formulário não é pré-preenchido previamente e cada campo é editável. Forneça o nome da pessoa que vai aceitar a entrega do dispositivo no campo Atenção. Ao escolher o local de entrega, considere o peso do dispositivo (66 lb. com sua caixa) e a acessibilidade.

   O dispositivo está equipado com rodas e alça retrátil para manuseio.
   {:note}

   - **Contatos de migração de chave**: esse formulário não é pré-preenchido. Cada campo é editável. Mais de uma pessoa pode ser incluída.
   - **Configuração de rede do data center**: forneça os detalhes de configuração de rede para o pré-fornecimento da porta Eth3 no dispositivo Mass Data Migration antes da remessa.
   - **Destino de transferência de dados**: selecione sua conta de destino existente na lista.
   - **Nome da solicitação**: insira um nome para ajudar a rastrear seu pedido.
5. Selecione a caixa de seleção **Eu li e concordo com os termos integrais do Contrato do Mass Data Migration** após a leitura de cada contrato de prestação de serviços.
6. Clique em **Fazer solicitação** para enviar a solicitação. Clique em **Cancelar** para abandonar completamente o formulário e retornar para a página de entrada do Mass Data Migration.


## Preparação e remessa

Depois de enviar a solicitação, o status para o chamado de solicitação aparece como `Processing Request`. Quando sua Solicitação é aceita, a {{site.data.keyword.IBM}} começa a pré-configurar o próximo dispositivo disponível.

Quando o dispositivo está sendo preparado, o status na página [Solicitações ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/storage/mdms){:new_window} mostra `Preparando dispositivo` seguido por `Aguardando remessa`. Após sua
solicitação entrar no status `Aguardando remessa`, ela não poderá mais ser cancelada.

Quando o dispositivo é retirado em loja pela transportadora para ser enviado para o seu local, o status da Solicitação é atualizado para `Dispositivo enviado`. O número de rastreamento é compartilhado com você na seção **Detalhes da ordem** da página [Solicitações ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/storage/mdms){:new_window}.


## Recebendo e Conectando

1. O dispositivo chega pré-configurado para você. Uma configuração básica de [instrução de energização e conectividade](user-instructions.html) está incluída. <br/>

   O nome do usuário e a senha do conjunto de armazenamentos são fornecidos separadamente. Verifique os **Detalhes da solicitação** em suas [Solicitações ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/storage/mdms){:new_window} para as credenciais.
   {:note}
2. Aponte seu navegador para o endereço IP estático fornecido no formulário do pedido.
3. Efetue login, insira a senha para desbloquear o conjunto de armazenamentos vazio. <br/>

   Consulte os Detalhes da solicitação da sua página [Solicitações ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/storage/mdms){:new_window} para a senha.
   {:tip}
4. Monte o compartilhamento NFS em seu servidor.
5. Execute novamente seu inventário do DataShuttle para assegurar que quaisquer novos arquivos sejam capturados.

## Movendo os Dados
1. Execute a cópia DataShuttle para mover os dados.
2. Bloquear o conjunto de armazenamento.
3. Encerre normalmente o dispositivo Mass Data Migration.
4. Envie a caixa de volta para o Data Center do {{site.data.keyword.BluSoftlayer_full}} usando a etiqueta de remessa que foi fornecida.

Quando o dispositivo é devolvido para o {{site.data.keyword.BluSoftlayer}}, o status da solicitação muda para `Dispositivo recebido`.

## Transação e acesso

Durante o processo de transferência, o status da solicitação será exibido como `Transferindo dados`. O status muda novamente quando a migração para o depósito do {{site.data.keyword.objectstorageshort}} é concluída (`Transferência concluída`). Seus dados ficarão imediatamente acessíveis quando o
descarregamento de alta velocidade no seu depósito do Cloud Object Storage for concluído.

## Apagando o Dispositivo

A {{site.data.keyword.IBM}} implementa os requisitos de limpeza de dados do Nível de DOD para apagar permanentemente seus dados do dispositivo. Quando concluído, o status da Solicitação exibe `Erase Complete`.