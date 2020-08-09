FT Wordpress
============

Objetivo
--------

Projeto para Criação de Imagens com tecnologias focado no uso da FT Networks porém aberta a comunidade.

Especificações do Container
---------------------------

* Tag `ft:wordpress`: Imagem de Container com Wordpress para utilização em Docker, Kubernetes e afins.
	- **Imagem Base**: php-alpine
	- **Web Server**: apache2
	- **PHP**: php7
	- **CMS**: Wordpress Latest 
	- **Entrypoint**: httpd -D FOREGROUND

Docker Hub
----------

* [`Docker Hub - flaptrap/ft`](https://hub.docker.com/r/flaptrap/ft)

### Como Usar:
* Start Container
  ```bash
  docker container run -d -p 80:80 flaptrap/ft:{tag}
  ```
* Container Shell
  ```bash
  docker exec -ti {nome_container} sh
  ```

Créditos
--------

Tag `ft:wordpress` foi baseada na instalação do [Wordpress para Alpine](https://wiki.alpinelinux.org/wiki/WordPress)
