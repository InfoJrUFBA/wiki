Troubleshooting
===============

ERROR 1067 (42000)
------------------

A mensagem de erro completa:

~~~ bash
ERROR 1067 (42000) at line 328: Invalid default value for 'tabela_qualquer'
~~~

Isso tem relação com a variável [sql_mode](https://dev.mysql.com/doc/refman/5.7/en/sql-mode.html). Nela tem os valores `NO_ZERO_IN_DATE,NO_ZERO_DATE`, dê uma olhada:

~~~ sql
mysql> show variables like 'sql_mode';
~~~

Você precisará modificá-la. Pode fazer de duas formas:

~~~ sql
SET sql_mode = ''
~~~

Mas assim não será persistente. Para persistir essa configuração você terá de editar o arquivo de configuração do MySQL. Provavelmente está em `/etc/mysql/`. Nesse diretório ficam os arquivos de configuração do MySQL. Você só terá de abrir e verificar o conteúdo. Mas, por padrão, costuma ser o arquivo `/etc/mysql/mysql.conf.d/mysqld.cnf`, pois tem as configurações do daemon do MySQL.

Então, basta adicionar a configuração da variável na seção sobre o MySQLd:

~~~
[mysqld]
sql_mode = 'sua configuração aqui'
~~~

E então é só reiniciar o serviço:

~~~
$ sudo service mysql restart
~~~
