# GIT / GIT HUB
# Usando 2 contas GIT na mesma máquina
# Using 2 GIT accounts on the same machine

## 🔹Configuração Inicial (Executar uma vez) / Initial Setup (Run once)

⚙️ PT - Quando precisamos utilizar 2 contas do git na mesma máquina, uma com as credenciais pessoais e outra com as credenciais de trabalho, precisamos realizar uma operação de host entre as contas. Na tentativa de ajudar compilei abaixo um processo para que todos possam condigurar suas máquinas para este processo, e claro aceito sugestões. (Este processo é devido apenas para pessoas que precisam ter commits em nomes e credenciais diferentes, se você usa 2 gits em apenas uma máquina mas realiza commits e pushs apenas de uma conta, não é ncessário fazer este processo)

⚙️ EN - When we need to use two Git accounts on the same machine, one with personal credentials and the other with work credentials, we need to perform a host operation between the accounts. In an attempt to help, I've compiled a process below so that everyone can configure their machines for this process, and of course, suggestions are welcome. (This process is only necessary for people who need to commit under different names and credentials; if you use two Git instances on a single machine but only commit and push from one account, this process is not required.)

## 🔹Passo 1 / Step 1

Para usarmos 2 contas do git no mesmo computador devemos criar a chave ssh de forma separada.  
_To use two Git accounts on the same computer, we must create separate SSH keys._

Consulte suas chaves SSH que hoje você tem em sua máquina. Utilize o comando no bash.  
_Check the SSH keys you currently have on your machine. Use the command in bash._

```python
ls -al ~/.ssh
```

Caso você não tenha nenhuma chave SSH Criada, não aparecerá nada. Se você ja tem, elas serão listadas com o comando acima.  
_If you don't have any SSH keys created, nothing will appear. If you already have them, they will be listed with the command above._

Para gerar uma chave ssh você deve usar o comando abaixo.  
_To generate an SSH key, you must use the command below._

```python
ssh-keygen -t ed25519 -C "user.email" -f ~/.ssh/id_ed25519_"Key_Name"
```

Para gerar uma segunda chave SSH, os nomes das chaves devem ser diferentes, logo você pode personalizar com o mesmo comando, mudando o "nome da chave", ao final do código.  
_To generate a second SSH key, the key names must be different, so you can customize it with the same command, changing the "key name" at the end of the code._

```python
ssh-keygen -t ed25519 -C "user.email" -f ~/.ssh/id_ed25519_"Key_Name_2"
```

Isto fará com que tenhamos 2 chaves cadastradas em nosso computador. Você pode checar as chaves no caminho  
C:\Users\seu.usuario\.ssh  
_This will result in us having 2 keys registered on our computer. You can check the keys in the path  
C:\Users\your.username\.ssh_

## 🔹Passo 2 / Step 2

Nomeando as 2 chaves de forma diferente teremos que criar um host para chavear os comandos do git hub. No mesmo diretório que temos as chaves SSH, (C:\Users\seu.usuario\.ssh), precisamos criar um arquivo config.  
_By naming the two keys differently, we will have to create a host to manage the GitHub commands. In the same directory where we have the SSH keys (C:\Users\your.username\.ssh), we need to create a config file._

```Python
touch .ssh/config
```

Ao criar o arquivo, abra-o com o vscode, ou algum outro software de edição de codigos, você deve digitar o codigo abaixo e substituir conforme seus nomes de chaves.  
_When creating the file, open it with VS Code, or some other code editing software, and type the code below, replacing the keys according to their names._

```Python
# New SSH configuration
Host github.com-"Key_Name_2"
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_"Key_Name_2"
```

Pulando uma linha, se pode adicionar quantos hosts precisarmos, mas a atenção aqui é endereçar a chave correta para cada bloco de códigos.  
_By skipping a line, you can add as many hosts as you need, but the important thing here is to address the correct key for each block of code._

## 🔹Passo 3 / Step 3

Vamos ao github no repositório que você deseja clonar e copiar a chave SSH do repositório  
_Go to the GitHub repository you want to clone and copy the repository's SSH key._

❗Atenção❗Agora quando clonamos um repositório devemos apenas incluir o host diretamente no link de clonagem, como no exemplo abaixo  
_❗Attention❗ Now, when cloning a repository, we should only include the host directly in the cloning link, as in the example below._

Antes, (Modo normal sem o host)  
_Previously, (Normal mode without host)_


```Python
git@github.com:repository.name/000_start.git
```

Depois, (com o host no config criado)  
_Then, (with the host in the config created)_

```Python
git@github.com"-Nome da New Key":repository.name/000_start.git
```

Agora, em cada repositório você deve configurar seu nome e email especifico para que você possa utilizar o host para executar seus commits e pushs de forma separada,  
_Now, in each repository you must configure your specific name and email so that you can use the host to execute your commits and pushes separately._

```Python
git config user.name
```
```Python
git config user.email
```
Para conferir qual nome esta em cada repositório use  
_To check which name is in each repository use_


```Python
git config user.name
```
```Python
git config user.email
````

Espero te ajudado nesta configuração!  
_I hope I helped you with this setup!_