### **1\. Verificar se o Docker está instalado**

Execute o comando abaixo para verificar se o Docker já está disponível no sistema:

bash

Copiar código

`docker --version`

-   **Se o Docker não estiver instalado**, siga o próximo passo.
-   **Se o Docker estiver instalado**, pode usar diretamente os comandos relacionados (veja a secção 3).

* * * * *

### **2\. Instalar o Docker (caso necessário)**

Se o Docker não estiver instalado, instale-o com os seguintes passos:

#### **Atualizar pacotes**

bash

Copiar código

`apt update && apt upgrade -y`

#### **Instalar pacotes necessários**

bash

Copiar código

`apt install -y apt-transport-https ca-certificates curl software-properties-common`

#### **Adicionar o repositório do Docker**

bash

Copiar código

`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`

#### **Instalar o Docker**

bash

Copiar código

`apt update
apt install -y docker-ce docker-ce-cli containerd.io`

#### **Verificar se o Docker está em execução**

bash

Copiar código

`systemctl start docker
systemctl enable docker
docker --version`

* * * * *

### **3\. Usar o Docker**

#### **Listar containers em execução**

bash

Copiar código

`docker ps`

#### **Listar todos os containers (inclusive os parados)**

bash

Copiar código

`docker ps -a`

#### **Acessar um container**

Se souber o nome ou ID do container, use:

bash

Copiar código

`docker exec -it <CONTAINER_ID> bash`

#### **Executar uma imagem Docker**

Para rodar uma nova imagem:

bash

Copiar código

`docker run -it ubuntu bash`

* * * * *

### **4\. Configurar permissões para evitar usar `root`**

Se quiser usar Docker sem ser o `root`:

1.  Adicione seu usuário ao grupo `docker`:

    bash

    Copiar código

    `usermod -aG docker $USER`

2.  Saia e entre novamente na sessão SSH para aplicar as mudanças.

Agora, pode executar comandos Docker sem privilégios de root.

Se precisar de mais ajuda, é só dizer!
