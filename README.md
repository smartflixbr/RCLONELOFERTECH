# Como Usar o Rclone para Montar Discos em Servidores Ubuntu 2024

---

Se você quiser montar serviços de armazenamento em nuvem como Google Drive, MEGA, OneDrive, e outros em um servidor Ubuntu, o **Rclone** é uma ferramenta poderosa e versátil para essa tarefa. Siga os passos abaixo para configurar e montar discos usando o Rclone no Ubuntu Server em 2024.

---
### O que é o Rclone:

O Rclone é uma ferramenta projetada para gerenciar e sincronizar dados entre vários serviços de armazenamento em nuvem e sistemas de arquivos locais. A ferramenta pode ser instalada em seus sistemas/servidores e conectada facilmente a vários armazenamentos em nuvem, como Amazon S3, Google Drive, Mega, Open Drive, Dropbox e muitos outros. Você só precisa configurar o seu armazenamento e obter um diretório extra diretamente na sua lista local com os conteúdos. É incrível. A ferramenta é útil para provedores de streaming que usam Xtream UI, XUI.ONE ou outros painéis, pois eles não precisam ter os arquivos localmente para serem selecionados e usados, já que essas nuvens podem ser utilizadas.

Eu vou abordar a versão do Rclone para Linux (Ubuntu) e configurar esses serviços um por um junto com meus vídeos no YouTube.

### Instalar o Rclone no Ubuntu:

Faça login no seu servidor via SSH e abra o terminal. Execute o seguinte comando, e a versão mais recente do Rclone será instalada e estará pronta para uso:

```bash
apt install zip unzip curl ; curl -O https://downloads.rclone.org/rclone-current-linux-amd64.zip ; unzip rclone-current-linux-amd64.zip ; cd rclone-*-linux-amd64 ; sudo cp rclone /usr/bin/ ; sudo chown root:root /usr/bin/rclone ; sudo chmod 755 /usr/bin/rclone ; rclone version
``` 

A saída deve ser informações sobre a versão que você acabou de instalar. Portanto, o Rclone está agora pronto, e precisamos começar a configurar os armazenamentos em nuvem um por um.

Vamos começar com o MEGA.NZ e, em seguida, continuar com os outros provedores de armazenamento à medida que vou criando vídeos sobre eles.

### Configurar o Rclone para MEGA.NZ no Ubuntu:

A seguir está o vídeo sobre como configurar corretamente o armazenamento com o Rclone, explicado de forma fácil e passo a passo:

Então, vamos começar o processo via SSH.

Execute o seguinte comando para abrir a configuração do Rclone:
