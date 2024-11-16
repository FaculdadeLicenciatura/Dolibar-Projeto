### **1\. Pré-requisitos**

Certifique-se de que seu sistema possui os pacotes necessários:

1.  **Atualize o sistema:**

    bash

    Copiar código

    `sudo apt update && sudo apt upgrade -y`

2.  **Instale o Apache, PHP e MySQL:** Dolibarr precisa de um servidor web, PHP e uma base de dados:

    bash

    Copiar código

    `sudo apt install -y apache2 mariadb-server php libapache2-mod-php php-cli php-common php-mysql php-json php-curl php-intl php-mbstring php-xml php-zip php-gd unzip wget`

3.  **Inicie e ative os serviços:**

    bash

    Copiar código

    `sudo systemctl start apache2
    sudo systemctl enable apache2
    sudo systemctl start mariadb
    sudo systemctl enable mariadb`

4.  **Configure o MySQL:** Configure a base de dados MySQL com o script de segurança:

    bash

    Copiar código

    `sudo mysql_secure_installation`

    -   Defina uma senha de root.
    -   Responda "Y" às perguntas para reforçar a segurança.

* * * * *

### **2\. Criar Base de Dados para o Dolibarr**

1.  Acesse o MySQL:

    bash

    Copiar código

    `sudo mysql -u root -p`

2.  Crie a base de dados e o usuário:

    sql

    Copiar código

    `CREATE DATABASE dolibarr_db CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
    CREATE USER 'dolibarr_user'@'localhost' IDENTIFIED BY 'senha_forte';
    GRANT ALL PRIVILEGES ON dolibarr_db.* TO 'dolibarr_user'@'localhost';
    FLUSH PRIVILEGES;
    EXIT;`

* * * * *

### **3\. Baixar e Instalar o Dolibarr**

1.  **Baixe o Dolibarr:**

    bash

    Copiar código

    `wget https://sourceforge.net/projects/dolibarr/files/latest/download -O dolibarr.zip`

2.  **Extraia os arquivos:**

    bash

    Copiar código

    `unzip dolibarr.zip -d /var/www/html/`

3.  **Renomeie o diretório para algo mais amigável:**

    bash

    Copiar código

    `sudo mv /var/www/html/dolibarr-* /var/www/html/dolibarr`

4.  **Defina permissões adequadas:**

    bash

    Copiar código

    `sudo chown -R www-data:www-data /var/www/html/dolibarr
    sudo chmod -R 755 /var/www/html/dolibarr`

* * * * *

### **4\. Configurar o Apache**

1.  Crie um arquivo de configuração para o Dolibarr:

    bash

    Copiar código

    `sudo nano /etc/apache2/sites-available/dolibarr.conf`

2.  Adicione o seguinte conteúdo:

    apache

    Copiar código

    `<VirtualHost *:80>
        ServerAdmin admin@yourdomain.com
        DocumentRoot /var/www/html/dolibarr/htdocs
        ServerName yourdomain.com

        <Directory /var/www/html/dolibarr/htdocs>
            Options FollowSymlinks
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/dolibarr_error.log
        CustomLog ${APACHE_LOG_DIR}/dolibarr_access.log combined
    </VirtualHost>`

3.  Ative o site e o módulo `rewrite`:

    bash

    Copiar código

    `sudo a2ensite dolibarr.conf
    sudo a2enmod rewrite
    sudo systemctl reload apache2`

* * * * *

### **5\. Configuração via Interface Web**

1.  Acesse o Dolibarr no navegador:

    perl

    Copiar código

    `http://<seu-endereço-IP>/install/`

2.  Siga o assistente de instalação para:

    -   Verificar os pré-requisitos.
    -   Configurar a base de dados (use `dolibarr_db`, `dolibarr_user` e a senha criada).
    -   Criar o usuário administrador.
3.  Após a instalação, **remova o diretório de instalação por segurança**:

    bash

    Copiar código

    `sudo rm -rf /var/www/html/dolibarr/install/`

* * * * *


Agora o **Dolibarr** está pronto para uso! Se precisar de ajuda com configurações adicionais ou personalização, é só pedir. 😊
