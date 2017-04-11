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
