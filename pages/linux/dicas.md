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
