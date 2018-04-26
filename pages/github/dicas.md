Dicas
=====

Configurar _deploy key_
-----------------------

Uma `deploy key` é uma chave SSH que configura-se em um repositório (unicamente!) para que se possa utilizar o protocolo SSH com ele.

**Não é permitido utilizar uma mesma chave SSH para dois repositórios**. Para saber onde mais você está utilizando a chave SSH, rode o comando:

~~~
$ ssh -T -ai ~/.ssh/id_rsa git@github.com
~~~

Em que `~/.ssh/id_rsa` é o endereço da chave SSH.

Para configurar uma chave dessas em um repositório você precisará ter uma chave SSH. Para saber como gerar visite [essa página](https://infojrufba.github.io/wiki/index.html#!pages/linux/dicas.md#Gerar_chaves_SSH).

Depois, copie a chave pública e insira no campo devido na seguinte página: https://github.com/InfoJrUFBA/wiki/settings/keys/new

Você consegue chegar até essa página seguindo o caminho: `Repositório > Settings > Deploy Keys > Add new`.