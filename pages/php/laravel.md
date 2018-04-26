Configuração
============

Criar chave de encriptação
--------------------------

~~~
$ php artisan key:generate
~~~

Rodar _migrations_ e _seeds_
----------------------------

| Comando | Função |
|---------|--------|
| php artisan migrate | Rodar _migrations_ |
| php artisan db:seed | Rodar _seeds_ |
| php artisan migrate --seed | Rodar _migrations_ e _seeds_ |

Aqui a documentação das [_migrations_](https://laravel.com/docs/5.6/migrations) e das [_seeds_](https://laravel.com/docs/5.6/seeding).

Rodar servidor
--------------

Você pode rodar o servidor interno do `artisan` para servir o Laravel:

~~~
$ php artisan serve --host 0.0.0.0
~~~