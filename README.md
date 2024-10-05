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

Link do video: https://www.youtube.com/watch?v=yyEsdWOJUl0

Então, vamos começar o processo via SSH.

Execute o seguinte comando para abrir a configuração do Rclone:

```bash
rclone config
```

Agora, você precisa responder primeiro com `n`, que significa nova configuração:

```bash
n
```

Responda com o nome do armazenamento (que será usado para identificação posteriormente; é recomendado usar o nome da empresa de armazenamento, como Mega):

```bash
Mega
```

Agora você verá uma lista de provedores e seus serviços que o Rclone suporta. Observe atentamente e responda com o número correspondente ao provedor.

No nosso caso, é 29 para Mega, então, responda com 29.

```bash
29
```

Agora, ele solicitará as credenciais da Mega. Responda com o seu e-mail da conta Mega:

```bash
mega-email@email.com
```

Agora, ele pedirá a senha. Responda com `1` para adicionar sua própria senha que você usa para entrar na sua conta Mega:

```bash
1
```

Responda novamente com a senha da conta Mega:

```bash
password
```

Agora está perguntando se você deseja editar as configurações avançadas. Com certeza não, então responda com `2` (acho que é isso, responda conforme apropriado):

```bash
2
```

Agora ele está perguntando se está tudo ok e se devemos salvar este provedor. Responda com `1` para sim:

```bash
1
```

E finalmente, saia do menu de configuração do Rclone respondendo com `q`, que significa sair:

```bash
q
```

Ainda temos muito mais a fazer, ah sim, na verdade. Execute o seguinte comando para evitar erros do fusermount:

```bash
sudo ln -s /bin/fusermount /bin/fusermount3
```

Após isso, precisamos primeiro criar uma pasta no nosso servidor que será usada para montar o armazenamento da Mega. Crie uma se você ainda não tiver:

```bash
mkdir -p /mega
```

Agora que nossa pasta está criada, precisamos montar nosso diretório Mega nesta pasta de forma permanente. Para isso, precisamos configurar um comando de execução automática no crontab da seguinte maneira:

### Configurar o Autoinício do serviço.

Eu criei um script para você facilitar essa tarefa rapidamente pelo terminal. Execute o seguinte comando, que abrirá uma lista de menus. Escolha "Adicionar novo serviço", escreva o nome do armazenamento em nuvem que você configurou no Rclone e escolha o diretório correspondente no seu servidor. O script fará o restante do trabalho. Uma vez concluído, você deverá ver o conteúdo no seu servidor e tudo estará configurado automaticamente.

Você pode facilmente adicionar mais serviços, editar ou excluí-los. Apenas lembre-se de escolher um diretório novo para o Rclone; caso contrário, isso pode prejudicar seus dados existentes no diretório do seu servidor.

```bash
wget lofertech.com/scripts/rclone.sh ; bash rclone.sh
```

Recarregue o daemon com o seguinte comando:

```bash
sudo systemctl daemon-reload
```

### Ative o serviço usando o seguinte comando:

```bash
sudo systemctl enable rclone1.service
```

Agora é hora de iniciar. Execute o seguinte comando e veja se você consegue ver o conteúdo no diretório:

```bash
sudo systemctl start rclone1.service
```

### Abaixo estão os comandos caso você precise reiniciar ou verificar o status:

Para reiniciar o serviço:

```bash
sudo systemctl start rclone1.service
```

Para parar o serviço:

```bash
sudo systemctl stop rclone1.service
```

Para verificar o status do serviço:

```bash
sudo systemctl status rclone1.service
```

### finalizando...
Abaixo está o comando completo que você pode precisar. O `mega:` é o nome do armazenamento que você configurou no terminal e `/mega` é o nome do diretório no servidor. Certifique-se de que eles correspondam. Se você executar este comando, pará-lo e não conseguir fazê-lo funcionar novamente, precisará matar o ID do processo ou reiniciar o servidor.

```bash
rclone mount mega: /mega --copy-links --no-gzip-encoding --no-check-certificate --allow-other --allow-non-empty --umask 000 --vfs-cache-mode writes
```

Verifique no terminal se o diretório do seu armazenamento em nuvem foi carregado corretamente:

```bash
ls /mega
```

Agora você deve ver a lista de diretórios e arquivos disponíveis dentro do seu terminal. Se não estiver tudo certo, tente executar o seguinte comando e verifique o diretório em algum software FTP, como o WinSCP.
