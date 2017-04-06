Dicas
=====

Substituição em massa em arquivos PHP
-------------------------------------

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

Copiar arquivos remotamente
---------------------------

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
