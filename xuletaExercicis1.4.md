# 0614 - UF1: A3: Comprovació de la instal·lació del servidor web Apache

## Enunciat


=== "Apache"

    1.- Anem a **canviar la configuració del servidor web** per tal que tinguem accessibles:

    * [http://ipDelServidor.cat/info.php](http://ipDelServidor.cat/info.php){target="_blank"}: 
        
        Tenint en compte tenim el fitxer `info.php` que ens mostra la informació del php - *phpinfo()* - del nostre servidor al directori apuntat per `DocumentRoot`
    
    * [http://ipDelServidor.cat/prova1](http://ipDelServidor.cat/prova1){target="_blank"}:
    
        On *prova1* és un directori creat dins el directori apuntat per `DocumentRoot` amb un fitxer `index.html` o `index.php` dins seu, accessible.

    * [http://ipDelServidor.cat/prova2/](http://ipDelServidor.cat/prova2/){target=_blank"}

        On *prova2* és un directori creat dins el directori `/var/www` i per tant hi accedim a través d'un *àlies* (*directori virtual*). Ha de ser accessible i contenir unes quantes imatges de les que se'ns n'ha de presentar un llistat. **No hi ha d'haver fitxer `index.php` ni `index.html`**. Per defecte, ha de mostar un llistat de les imatges/fitxers del directori.

    * [http://ipDelServidor.cat/prova3/](http://ipDelServidor.cat/prova3/){target=_blank"}

        [http://ipDelServidor.cat/prova3/imatge.png](http://ipDelServidor.cat/prova3/imatge.png){target=_blank"}
        
        On *prova3* és un directori creat dins el directori `/var/www` i per tant hi accedim a través d'un *àlies* (*directori virtual*). Ha de ser accessible i contenir Com a mínim una imatge amb el nom `imatge3.png`. **No hi ha d'haver fitxer `index.php` ni `index.html`**. No ha de mostar cap imatge per defecte sinó la pàgina de l'error 403.

=== "Nginx"

    1.- Anem a **canviar la configuració del servidor web** per tal que tinguem accessibles:

    * [http://ipDelServidor.cat/info.php](http://ipDelServidor.cat/info.php){target="_blank"}: 
        
        Tenint en compte tenim el fitxer `info.php` que ens mostra la informació del php - *phpinfo()* - del nostre servidor al directori apuntat per `root`
    
    * [http://ipDelServidor.cat/prova1](http://ipDelServidor.cat/prova1){target="_blank"}:
    
        On *prova1* és un directori creat dins el directori apuntat per `root` amb un fitxer `index.html` o `index.php` dins seu, accessible.

    * [http://ipDelServidor.cat/prova2/](http://ipDelServidor.cat/prova2/){target=_blank"}

        On *prova2* és un directori creat dins el directori `/var/www` i per tant hi accedim a través d'un *àlies* (*directori virtual*). Ha de ser accessible i contenir unes quantes imatges de les que se'ns n'ha de presentar un llistat. **No hi ha d'haver fitxer `index.php` ni `index.html`**. Per defecte, ha de mostar un llistat de les imatges/fitxers del directori.

    * [http://ipDelServidor.cat/prova3/](http://ipDelServidor.cat/prova3/){target=_blank"}

        [http://ipDelServidor.cat/prova3/imatge.png](http://ipDelServidor.cat/prova3/imatge.png){target=_blank"}
        
        On *prova3* és un directori creat dins el directori `/var/www` i per tant hi accedim a través d'un *àlies* (*directori virtual*). Ha de ser accessible i contenir Com a mínim una imatge amb el nom `imatge3.png`. **No hi ha d'haver fitxer `index.php` ni `index.html`**. No ha de mostar cap imatge per defecte sinó la pàgina de l'error 403.

Demostra a través de captures:

* els canvis a la modificació del servidor web mostrant canvis en els fitxers de configuració dl servidor, indicant en tot moment el fitxer que estem modificant

* l'accés des del teu navegador web a les pàgines anteriors.

## Possible solució

=== "Apache"

    La solució que es donarà a continuació serà modificant única i exclusivament el fitxer `/etc/apache2/sites-available/000-default.conf`.

    Després de cada canvi caldria comprovar la sintaxis dels fitxers de configuració i en cas de ser correcte reiniciar el servidor web. Això podem fer-ho en una sola comanda des de la *shell* de la següent forma

    ``` doscon
    sudo apache2ctl -t && sudo systemctl restart apache2
    ```
    ### [http://ipDelServidor.cat/info.php](http://ipDelServidor.cat/info.php){target="_blank"}:

    ??? "Enunciat -> [http://ipDelServidor.cat/info.php](http://ipDelServidor.cat/info.php){target="_blank"}"
        
        Tenint en compte que tenim el fitxer `info.php` que ens mostra la informació del php - *phpinfo()* - del nostre servidor al directori apuntat per `DocumentRoot`

    ??? "Solució -> [http://ipDelServidor.cat/info.php](http://ipDelServidor.cat/info.php){target="_blank"}"

        En aquest cas **no cal fer cap canvi** sempre i quan tinguem instal·lat i activat el *mòdul `php`*. L'únic que cal és copiar el fitxer [info.php](docs/info.php) al directori `/var/www/html`.

        ``` doscon hl_lines="1 4"
        ls /var/www/html/info.php
        /var/www/html/info.php
        
        cat /var/www/html/info.php
        <?php
            phpinfo();
        ?>
        ```

    ### [http://ipDelServidor.cat/prova1](http://ipDelServidor.cat/prova1){target="_blank"}:

    ??? "Enunciat -> [http://ipDelServidor.cat/prova1](http://ipDelServidor.cat/prova1){target="_blank"}"

        On *prova1* és un directori creat dins el directori apuntat per `DocumentRoot` amb un fitxer `index.html` o `index.php` dins seu, accessible.

    ??? "Solució -> [http://ipDelServidor.cat/prova1](http://ipDelServidor.cat/prova1){target="_blank"}"

        En aquest cas **no cal fer cap canvi** sempre i quan tinguem creat el directori `prova1` dins el directori apuntat per la directiva `DocumentRoot`. Dins del directori hi afegirem un fitxer `index.html` que ens mostri on estem.

        ``` doscon hl_lines="1 2"
        sudo mkdir /var/www/html/prova1
        sudo nano /var/www/html/prova1/index.html
        ```

        ``` html
        <html>
            <head>
                <title>Pàgina de la prova1</title>
                <meta charset="utf8">
            </head>
            <body>
                <h1>prova1</h1>
                <p>Et trobes al directori <b><i>prova1</i></b></p>
                <p>Benvingut/da!!!</p>
            </body>
        </html>
        ```
        [![Accés web](img/a3Sol001.png)](img/a3Sol001.png){target="_blank"}

    ### [http://ipDelServidor.cat/prova2/](http://ipDelServidor.cat/prova2/){target=_blank"}

    ??? "Enunciat -> [http://ipDelServidor.cat/prova2/](http://ipDelServidor.cat/prova2/){target=_blank"}"

        On *prova2* és un directori creat dins el directori `/var/www` i per tant hi accedim a través d'un *àlies* (*directori virtual*). Ha de ser accessible i contenir unes quantes imatges de les que se'ns n'ha de presentar un llistat. **No hi ha d'haver fitxer `index.php` ni `index.html`**.

    ??? "Solució -> [http://ipDelServidor.cat/prova2/](http://ipDelServidor.cat/prova2/){target=_blank"}"

        El primer que cal fer és **crear el directori físic dins de `/var/www`**. Per això podem executar la comanda de creació del directori _des del ssh_

        Caldrà assegurar-nos que l'usuari `www-data` hi té permís de lectura. Per defecte els permisos són `-rwxr-xr-x` per tant ja és correcte.

        **Des de la Shell**

        ``` doscon hl_lines="1 2"
        sudo mkdir /var/www/prova2
        ls -ld /var/www/prova2
        drwxr-xr-x 1 root root 4096 Mmm dd hh:mm /var/www/prova2
        ```

        Com que aquest directori no està per sota del directori indicat a la directiva `DocumentRoot` cal crear un _directori virtual_ o _alias_. Per això editarem el fitxer `/etc/apache2/sites-available/000-default.conf` i entre les etiquetes `<VirtualHost>` i `</VirtualHost>` afegirem les següents línies:

        ``` apache hl_lines="1-3 5"
        Alias /prova2 /var/www/prova2
        <Directory /var/www/prova2>
            Options +Indexes
            Require all granted
        </Directory>
        ```

        Ara *només ens queda reiniciar el servei web* amb la comanda `systemctl restart apache2`

        [![Accés web](img/a3Sol002apache.png)](img/a3Sol002apache.png){target="_blank"}


    ### [http://ipDelServidor.cat/prova3/](http://ipDelServidor.cat/prova3/){target=_blank"}

    ??? "Enunciat -> [http://ipDelServidor.cat/prova3/](http://ipDelServidor.cat/prova3/){target=_blank"} i [http://ipDelServidor.cat/prova3/imatge.png](http://ipDelServidor.cat/prova3/imatge.png){target=_blank"}"
        
        On *prova3* és un directori creat dins el directori `/var/www` i per tant hi accedim a través d'un *àlies* (*directori virtual*). Ha de ser accessible i contenir Com a mínim una imatge amb el nom `imatge3.png`. **No hi ha d'haver fitxer `index.php` ni `index.html`**.

    ??? "Solució -> [http://ipDelServidor.cat/prova3/](http://ipDelServidor.cat/prova3/){target=_blank"} i [http://ipDelServidor.cat/prova3/imatge.png](http://ipDelServidor.cat/prova3/imatge.png){target=_blank"}"

        El primer que cal fer és **crear el directori físic dins de `/var/www`**. Per això podem executar la comanda de creació del directori _des del ssh_

        Caldrà assegurar-nos que l'usuari `www-data` hi té permís de lectura. Per defecte els permisos són `-rwxr-xr-x` per tant ja és correcte.

        **Des de la shell**

        ``` doscon hl_lines="1 2"
        sudo mkdir /var/www/prova3
        ls -ld /var/www/prova3
        drwxr-xr-x 1 root root 4096 Mmm dd hh:mm /var/www/prova
        ```

        Com que aquest directori no està per sota del directori indicat a la directiva `DocumentRoot` cal crear un _directori virtual_ o _alias_. Per això editarem el fitxer `/etc/apache2/sites-available/000-default.conf` i entre les etiquetes `<VirtualHost>` i `</VirtualHost>` afegirem les següents línies:

        ``` apache hl_lines="1-3 5"
        Alias /prova3 /var/www/prova3
        <Directory /var/www/prova3>
            Options -Indexes
            Require all granted
        </Directory>
        ```

        També afegirem una imatge dins el directori `/var/www/prova3`

        ```bash
        sudo wget https://ih1.redbubble.net/image.1089399808.4161/raf,360x360,075,t,fafafa:ca443f4786.jpg -O /var/www/prova3/imatge.png
        ```

        Ara *només ens queda reiniciar el servei web* amb la comanda `systemctl restart apache2`

        [![Accés web](img/a3Sol003apache.png)](img/a3Sol003apache.png){target="_blank"}

=== "Nginx"

    La solució que es donarà a continuació serà modificant única i exclusivament el fitxer `/etc/nginx/sites-available/default`.

    Després de cada canvi caldria comprovar la sintaxis dels fitxers de configuració i en cas de ser correcte reiniciar el servidor web. Això podem fer-ho en una sola comanda des de la *shell* de la següent forma

    ``` doscon
    sudo nginx -t && sudo systemctl restart nginx
    ```

    ### [http://ipDelServidor.cat/info.php](http://ipDelServidor.cat/info.php){target="_blank"}:

    ??? "Enunciat -> [http://ipDelServidor.cat/info.php](http://ipDelServidor.cat/info.php){target="_blank"}"
        
        Tenint en compte que tenim el fitxer `info.php` que ens mostra la informació del php - *phpinfo()* - del nostre servidor al directori apuntat per `root`

    ??? "Solució -> [http://ipDelServidor.cat/info.php](http://ipDelServidor.cat/info.php){target="_blank"}"

        En aquest cas **no cal fer cap canvi** sempre i quan tinguem instal·lat i activat el *servei `php-fpm`*. L'únic que cal és copiar el fitxer [info.php](docs/info.php) al directori `/var/www/html`.

        ``` doscon hl_lines="1 4"
        ls /var/www/html/info.php
        /var/www/html/info.php
        
        cat /var/www/html/info.php
        <?php
            phpinfo();
        ?>
        ```

    ### [http://ipDelServidor.cat/prova1](http://ipDelServidor.cat/prova1){target="_blank"}:

    ??? "Enunciat -> [http://ipDelServidor.cat/prova1](http://ipDelServidor.cat/prova1){target="_blank"}"

        On *prova1* és un directori creat dins el directori apuntat per `root` amb un fitxer `index.html` o `index.php` dins seu, accessible.

    ??? "Solució -> [http://ipDelServidor.cat/prova1](http://ipDelServidor.cat/prova1){target="_blank"}"

        En aquest cas **no cal fer cap canvi** sempre i quan tinguem creat el directori `prova1` dins el directori apuntat per la directiva `root`. Dins del directori hi afegirem un fitxer `index.html` que ens mostri on estem.

        ``` doscon hl_lines="1 2"
        sudo mkdir /var/www/html/prova1
        sudo nano /var/www/html/prova1/index.html
        ```

        ``` html
        <html>
            <head>
                <title>Pàgina de la prova1</title>
                <meta charset="utf8">
            </head>
            <body>
                <h1>prova1</h1>
                <p>Et trobes al directori <b><i>prova1</i></b></p>
                <p>Benvingut/da!!!</p>
            </body>
        </html>
        ```
        [![Accés web](img/a3Sol001nginx.png)](img/a3Sol001nginx.png){target="_blank"}

    ### [http://ipDelServidor.cat/prova2/](http://ipDelServidor.cat/prova2/){target=_blank"}

    ??? "Enunciat -> [http://ipDelServidor.cat/prova2/](http://ipDelServidor.cat/prova2/){target=_blank"}"

        On *prova2* és un directori creat dins el directori `/var/www` i per tant hi accedim a través d'un *àlies* (*directori virtual*). Ha de ser accessible i contenir unes quantes imatges de les que se'ns n'ha de presentar un llistat. **No hi ha d'haver fitxer `index.php` ni `index.html`**.

    ??? "Solució -> [http://ipDelServidor.cat/prova2/](http://ipDelServidor.cat/prova2/){target=_blank"}"

        El primer que cal fer és **crear el directori físic dins de `/var/www`**. Per això podem executar la comanda de creació del directori _des del ssh_

        Caldrà assegurar-nos que l'usuari `www-data` hi té permís de lectura. Per defecte els permisos són `-rwxr-xr-x` per tant ja és correcte.

        **Des de la Shell**

        ``` doscon hl_lines="1 2"
        sudo mkdir /var/www/prova2
        ls -ld /var/www/prova2
        drwxr-xr-x 1 root root 4096 Mmm dd hh:mm /var/www/prova2
        ```

        Com que aquest directori no està per sota del directori indicat a la directiva `root` cal crear un _directori virtual_ o _alias_. Per això editarem el fitxer `/etc/nginx/sites-available/default` i entre dins les claus del `server { ... }` afegirem les següents línies:

        ``` nginx hl_lines="1-3 5"
        location /prova2 {
            alias /var/www/prova2;
            autoindex on;
        }
        ```

        Ara *només ens queda reiniciar el servei web* amb la comanda `systemctl restart apache2`

        [![Accés web](img/a3Sol002nginx.png)](img/a3Sol002nginx.png){target="_blank"}


    ### [http://ipDelServidor.cat/prova3/](http://ipDelServidor.cat/prova3/){target=_blank"}

    ??? "Enunciat -> [http://ipDelServidor.cat/prova3/](http://ipDelServidor.cat/prova3/){target=_blank"} i [http://ipDelServidor.cat/prova3/imatge.png](http://ipDelServidor.cat/prova3/imatge.png){target=_blank"}"
        
        On *prova3* és un directori creat dins el directori `/var/www` i per tant hi accedim a través d'un *àlies* (*directori virtual*). Ha de ser accessible i contenir Com a mínim una imatge amb el nom `imatge3.png`. **No hi ha d'haver fitxer `index.php` ni `index.html`**.

    ??? "Solució -> [http://ipDelServidor.cat/prova3/](http://ipDelServidor.cat/prova3/){target=_blank"} i [http://ipDelServidor.cat/prova3/imatge.png](http://ipDelServidor.cat/prova3/imatge.png){target=_blank"}"

        El primer que cal fer és **crear el directori físic dins de `/var/www`**. Per això podem executar la comanda de creació del directori _des del ssh_

        Caldrà assegurar-nos que l'usuari `www-data` hi té permís de lectura. Per defecte els permisos són `-rwxr-xr-x` per tant ja és correcte.

        **Des de la shell**

        ``` doscon hl_lines="1 2"
        sudo mkdir /var/www/prova3
        ls -ld /var/www/prova3
        drwxr-xr-x 1 root root 4096 Mmm dd hh:mm /var/www/prova
        ```

        Com que aquest directori no està per sota del directori indicat a la directiva `root` cal crear un _directori virtual_ o _alias_. Per això editarem el fitxer `/etc/nginx/sites-available/default` i entre dins les claus del `server { ... }` afegirem les següents línies:

        ``` nginx hl_lines="1-3 5"
        location /prova3 {
            alias /var/www/prova3;
            autoindex off;
        }
        ```

        També afegirem una imatge dins el directori `/var/www/prova3`

        ```bash
        sudo wget https://ih1.redbubble.net/image.1089399808.4161/raf,360x360,075,t,fafafa:ca443f4786.jpg -O /var/www/prova3/imatge.png
        ```

        Ara *només ens queda reiniciar el servei web* amb la comanda `systemctl restart nginx`

        [![Accés web](img/a3Sol003nginx.png)](img/a3Sol003nginx.png){target="_blank"}


--8<-- ".acronims.txt"
