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

ERROR 1366 (HY000)
------------------

Saída completa do erro:

~~~
ERROR 1366 (HY000) at line 623: Incorrect string value: '\xF0\x9F\x98\x8A" ...'
~~~

Explicação:

> MySQL's utf8 permits only the Unicode characters that can be represented with 3 bytes in UTF-8. Here you have a character that needs 4 bytes: \xF0\x90\x8D\x83 (U+10343 GOTHIC LETTER SAUIL).
>
> If you have MySQL 5.5 or later you can change the column encoding from utf8 to utf8mb4. This encoding allows storage of characters that occupy 4 bytes in UTF-8.
>
> You may also have to set the server property character_encoding_server to utf8mb4 in the MySQL configuration file.
>
> [Fonte](http://stackoverflow.com/questions/10957238/incorrect-string-value-when-trying-to-insert-utf-8-into-mysql-via-jdbc)

Para resolver, como visto, só configurar o MySQL para `utf8mb4`. Para isso, edite o arquivo `/etc/mysql/my.cnf` colocando o seguinte conteúdo:

~~~
[mysql]
default-character-set=utf8mb4

[client]
default-character-set=utf8mb4

[mysqldump]
default-character-set=utf8mb4
~~~

E então reinicie o servidor:

~~~
$ sudo service mysql restart
~~~
