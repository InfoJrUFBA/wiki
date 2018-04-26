Dicas
=====

Baixar apenas uma branch
------------------------

Para baixar apenas uma branch do servidor, utilize o comando:

~~~
$ git clone --single-branch git_url
~~~

Isso é bom para quando vamos baixar um repositório grande mas só precisamos daquela branch que vai para testing/homologação/produção (ex. master).

Deletar branch remota
---------------------

Para deletar uma branch que está no servidor (ex. github.com) via terminal, basta dar um push seguindo essa sintaxe:

~~~
$ git push origin :branch_a_deletar
~~~

Upload renomeando branch
------------------------

Se quiser fazer upload de uma branch local, que se chama AAA, para o servidor chamando-a de BBB, basta fazer o seguinte:

~~~
$ git push origin AAA:BBB
~~~

Baixar submódulos
-----------------

Para baixar submódulos basta rodar o comando:

~~~
$ git submodule update --init
~~~

Isso serve como uma forma para baixar dependências, por exemplo.