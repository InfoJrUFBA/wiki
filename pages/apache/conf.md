Configuração
============

Bloqueio do .git
----------------

Adicione as linhas abaixo no arquivo de configuração padrão do apache:

~~~
RewriteEngine On
RedirectMatch 404 .*\.git.*
~~~

Isso irá prevenir acesso a qualquer arquivo do git (.git, .gitignore, .gitkeep), arquivos dentro do .git...

Proxy Reverso
-------------

Habilite os módulos necessários rodando os comandos abaixo como `root`:

~~~
a2enmod proxy
a2enmod proxy_http
a2enmod proxy_ajp
a2enmod rewrite
a2enmod deflate
a2enmod headers
a2enmod proxy_balancer
a2enmod proxy_connect
a2enmod xml2enc
a2enmod proxy_html
~~~

Teste as configurações:

~~~
$ apache2ctl configtest
~~~

Se estiver tudo certo, então reinicie o servidor:

~~~
# service apache2 restart
~~~

Depois, no `VirtualHost` necessário use a seguinte configuração:

~~~
<VirtualHost *:80>
    ProxyPreserveHost On

    ProxyPass / http://ip:[port]/
    ProxyPassReverse / http://ip:[port]/
    ServerName domain
    ServerAlias www.domain
</VirtualHost>
~~~

VirtualHost
-----------

Um conteúdo padrão para os arquivos de VirtualHost dos projetos é o seguinte:

~~~
<VirtualHost *:80>
	ServerName project.infojr.com.br
	ServerAlias www.project.infojr.com.br
	DocumentRoot /var/www/project/

	<Directory /var/www/project>
		AllowOverride All
		Options -Indexes
	</Directory>

	ErrorLog ${APACHE_LOG_DIR}/projects/project_error.log
	CustomLog ${APACHE_LOG_DIR}/projects/project_access.log combined
</VirtualHost>
~~~

Teste as configurações:

~~~
# apache2ctl configtest
~~~

Se estiver tudo `Ok`, reinicie o apache:

~~~
# service apache2 restart
~~~
