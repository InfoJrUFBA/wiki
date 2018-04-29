Dicas
=====

Comandos SQL úteis
------------------

| Descrição | Comando |
|-----------|---------|
| Criar banco de dados | `CREATE DATABASE database` |
| Criar usuário | `CREATE USER 'usuario'@'local.de.acesso' IDENTIFIED BY 'senhafortedousuario'` |
| Dar permissão ao usuário | `GRANT ALL ON bancodedados.* TO usuario@'local.de.acesso'` |
| Exibir permissões para determinado usuário | `show grants for 'usuario'@'local.de.acesso'` |
| Deletar usuário | `drop user 'usuario'@'local.de.acesso'` |
| Aplicar configuração de privilégios | `flush privileges` |

Apagar todos os schemas do banco de dados
-----------------------------------------

Primeiro, você tem de saber quais todos os schemas que tem no seu servidor:

~~~
$ echo "show databases;" | mysql -u root -p
~~~

Retirar os bancos padrões do MySQL (mysql, information_schema, Database, performance_schema) e então colocar na sintaxe de deletar o banco (`drop database schema_a_apagar`). Podemos juntar isso tudo em um comando para gerar um arquivo e depois executar esse arquivo no servidor:

~~~
$ mysql -u root -p -e "show databases;" | grep -v mysql | grep -v information_schema | grep -v Database | grep -v performance_schema | gawk '{print "drop database " $1 ";select sleep(0.1);"}' > delete.sql
~~~

E então:

~~~
$ cat delete.sql | mysql -u root -p
~~~

Executar vários arquivos sql
----------------------------

Você pode fazer isso de várias formas, por exemplo:

* Concatenar todos arquivos e executar apenas um;
* Copiar o conteúdo, arquivo por arquivo, e ir executando;
* Fazer um script para executar cada arquivo separado.

E é exatamente o último que vai ser mostrado aqui. Basta fazer uma listagem dos arquivos sql e então um loop em cada arquivo, executando-o, veja:

~~~
$ for i in `ls *.sql`; do echo $i; mysql -u root -p < $i; done;
~~~

Backup de todas bases de dados
------------------------------

Precisava fazer um backup, um dump, de todas as bases de dados que existia no banco MySQL, pois bem, aqui está o script que usei e funcionou bem:

~~~
$ for db in $(mysql -u root -p'PASSWORD' -e "show databases;" | grep -v '\(mysql\|information_schema\|Database\|performance_schema\)'); do mysqldump --single-transaction -u root -p'PASSWORD' $db > $db.sql; done
~~~
