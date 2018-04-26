Dicas
=====

Sed
---

### Substituição em massa em arquivos PHP

~~~ bash
for i in $(find . -regextype posix-egrep -regex '.*\.php'); do 
    sudo sed -i 's/<?php @eval($_POST\[.*\]);?>//g' $i; 
done
~~~

Esse comando faz um loop em todos arquivos PHP encontrados pelo `find` e faz a substituição pelo `sed`.

* Find
    * `-regextype`: Seta a configuração de expressão regular que o find irá utilizar
    * `-regex`: Seta a regex em seguida como o padrão a ser buscado
    * `'.*\.php'`: O padrão busca qualquer caractere em qualquer nível de repetição e finalizando com `.php`

* Sed
    * `-i`: Faz as mudanças interativamente, já editando os arquivos em momento de busca
    * `s///g`: `s` é o comando de busca e substituição e `g` marca para ser feito globalmente nos arquivos
    * `<?php @eval($_POST\[.*\]);?>`: Busca o padrão `<?php @eval($_POST[]);?>` sendo que dentro do post poderia ter qualquer caractere em qualquer quantidade

### Substituição com REGEX com grupos

~~~
$ sed -i 's/\(padrao\).*$/\1/' arquivo
~~~

SSH
---

### Acesso ao servidor

Quando precisamos entrar no servidor para configurá-lo normalmente utilizaremos o protocolo/aplicação [SSH](https://pt.wikipedia.org/wiki/Secure_Shell) ([RFC4251](https://tools.ietf.org/html/rfc4251), [RFC4252](https://tools.ietf.org/html/rfc4252), [RFC4253](https://tools.ietf.org/html/rfc4253)). Para isso, precisaremos de um cliente SSH e o cliente (recomendação pessoal) depende do seu sistema operacional:

* [GNU/Linux](https://linux.die.net/man/1/ssh)
* [Windows](https://www.putty.org/)

O processo de autenticação pode ser utilizando senha ou chaves SSH (para saber como criar as chaves, [clique aqui](https://infojrufba.github.io/wiki/index.html#!pages/linux/dicas.md#Gerar_chaves_SSH). Para entender melhor como funciona, [aqui](https://www.digitalocean.com/community/tutorials/understanding-the-ssh-encryption-and-connection-process)).

Vamos abordar melhor sobre o cliente SSH via linha de comando no GNU/Linux. Alguns parâmetros interessantes:

* `-p`: indica a porta que o servidor SSH está configurado;
* `-l`: indica o login que deve ser utulizado para autenticar. Padrão é ser o mesmo login da máquina local;
* `-i`: indica o endereço da chave SSH. Padrão é `~/.ssh/id_rsa`.

Exemplo de comando:

~~~
$ ssh -l gildasiojunior servidor.da.infojr.com.br
~~~

### Copiar arquivos remotamente

Isso é bastante útil quando se está trabalhando com servidores, seja para transferir arquivos entre sua máquina e um servidor ou entre dois servidores. É simples... Você vai usar um utilitário da suíte `ssh`, o `scp`.

A sintaxe é simples:

~~~
$ scp endereço_arquivo_copiado endereço_arquivo_colado
~~~

A diferença vai só como o endereço será mostrado: `usuario@servidor:/path`. Veja o exemplo:

* Copiando `/tmp/texto` do computador pessoal para o servidor `server`, com usuário `root` e salvando em `/var/www/html`:

~~~
$ scp /tmp/texto root@server:/var/www/html
~~~

Há alguns parâmetros interessantes, como por exemplo:

* `-i`: você pode colocar o caminho para uma chave ssh que lhe dá permissão de acessar a outra máquina;
* `-r`: copia recursivamente um diretório.

### Gerar chaves SSH

No GNU/Linux, para gerar uma chave SSH é bem simples. Rode o seguinte comando:

~~~
$ ssh-keygen
~~~

* Você *poderá* informar um local para salvar a chave SSH. Padrão é `~/.ssh`;
* Você *poderá* configurar uma senha para utilização da chave.

Usuários
--------

### Criar usuários

~~~
$ sudo adduser usuario
~~~

### Colocar usuário em um novo grupo

~~~
$ sudo usermod -a -G grupo usuario
~~~

Depois o usuário pode logar no grupo em uma sessão ativa (sem precisar fazer logoff) com o comando:

~~~
$ newgrp - grupo
~~~