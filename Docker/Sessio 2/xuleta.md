# Apache Server
**Link:** [https://chatgpt.com/c/68d44a00-c44c-8323-bb7c-4c9a12716673](https://chatgpt.com/c/68d44a00-c44c-8323-bb7c-4c9a12716673)  

## Response:
Perfecte 👌 Aquí tens un **esquema resum complet i clar** de la **instal·lació i estructura d’Apache2 a Ubuntu 24.04**, ideal per a estudiants o per repàs tècnic:

* * *

🧩 **Instal·lació bàsica d’Apache2 a Ubuntu 24.04**
---------------------------------------------------

### 🔹 1. Instal·lació

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install apache2 -y
```

Després de la instal·lació, el servei s’activa automàticament:

```bash
sudo systemctl status apache2
```

* * *

📁 **Estructura principal de carpetes i fitxers**
-------------------------------------------------

### 📂 `/etc/apache2/`
```bash
sudo systemctl status apache2
```

* * *

📁 **Estructura principal de carpetes i fitxers**
-------------------------------------------------

### 📂 `/etc/apache2/`

📍 **Directori principal de configuració d’Apache.**  
Conté tots els fitxers i carpetes que controlen el comportament del servidor.

* * *

### Subcarpetes importants:

| Carpeta / Fitxer | Descripció |
| --- | --- |
| **`/etc/apache2/apache2.conf`** | Fitxer de **configuració principal** del servidor. Inclou la resta de configuracions i defineix paràmetres globals. |
| **`/etc/apache2/envvars`** | Variables d'entorn utilitzades per Apache (usuari, grup, rutes de logs...). |
| **`/etc/apache2/ports.conf`** | Defineix **els ports** als quals Apache escolta (normalment 80 per HTTP i 443 per HTTPS). |
| **`/etc/apache2/sites-available/`** | Conté els **fitxers de configuració dels VirtualHosts disponibles**. (No actius per defecte.) |
| **`/etc/apache2/sites-enabled/`** | Conté enllaços simbòlics als fitxers **actius** de `sites-available`. |
| **`/etc/apache2/mods-available/`** | Conté tots els **mòduls disponibles** que es poden habilitar (com `rewrite`, `ssl`, `php`, etc.). |
| **`/etc/apache2/mods-enabled/`** | Conté enllaços simbòlics als mòduls **habilitats actualment**. |
| **`/etc/apache2/conf-available/`** | Configuracions addicionals disponibles (no específiques d’un lloc). |
| **`/etc/apache2/conf-enabled/`** | Enllaços simbòlics a les configuracions addicionals **activades**. |

* * *

### 🔹 2. Activació / desactivació de llocs i mòduls

| Acció | Comanda |
| --- | --- |
| Activar un VirtualHost | `sudo a2ensite nomdellloc.conf` |
| Desactivar un VirtualHost | `sudo a2dissite nomdellloc.conf` |
| Activar un mòdul | `sudo a2enmod modul` |
| Desactivar un mòdul | `sudo a2dismod modul` |
| Reiniciar servei | `sudo systemctl reload apache2` |

* * *

🌐 **Arbre de fitxers web per defecte**
---------------------------------------

| Ruta | Descripció |
| --- | --- |
| **`/var/www/html/`** | 📁 **Directori arrel (DocumentRoot)** per defecte on es guarden els fitxers web públics (`index.html`, etc.). |
| **`/var/www/`** | Pot contenir altres carpetes per a VirtualHosts o projectes addicionals. |

* * *

🔧 **Fitxer per defecte del lloc web**
--------------------------------------

| Fitxer | Localització | Funció |
| --- | --- | --- |
| **`/etc/apache2/sites-available/000-default.conf`** | Configuració del **VirtualHost per defecte**. Normalment apunta a `/var/www/html`. |  |

### Exemple del contingut bàsic:

```apache
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

* * *

🔒 **Altres directoris útils**
------------------------------

| Carpeta | Descripció |
| --- | --- |
| **`/var/log/apache2/`** | Fitxers de **logs** del servidor (`access.log`, `error.log`). |
| **`/usr/lib/apache2/`** | Conté els **mòduls binaris (.so)** del servidor. |
| **`/usr/share/apache2/`** | Fitxers compartits i documentació del servidor. |
| **`/run/apache2/`** | Fitxers de procés i sockets temporals. |

* * *

✅ **Resum visual**
------------------

```
/etc/apache2/
 ├── apache2.conf            → Config principal
 ├── ports.conf              → Ports (80, 443)
 ├── envvars                 → Variables d'entorn
 ├── sites-available/        → VirtualHosts disponibles
 │    └── 000-default.conf
 ├── sites-enabled/          → Enllaços als llocs actius
 ├── mods-available/         → Mòduls disponibles
 ├── mods-enabled/           → Mòduls actius
 ├── conf-available/         → Configs extra disponibles
 └── conf-enabled/           → Configs extra actives

/var/www/html/               → 📂 Arrel web (DocumentRoot per defecte)
/var/log/apache2/            → 🧾 Logs
```

* * *

Vols que t’afegeixi també un **esquema gràfic resumible per imprimir** (tipus full de recordatori o esquema visual per classe)?

## Response:
Perfecte 💪 Aquí tens un **resum complet, clar i pràctic** amb les **comandes bàsiques més útils per treballar amb un servidor Ubuntu Server**, especialment pensades per a **administrar Apache2** i fer configuracions bàsiques.

* * *

🧩 **Comandes bàsiques per a treballar en un servidor Ubuntu Server**
=====================================================================

🔹 **1\. Actualitzar el sistema**
---------------------------------

Mantenir el servidor al dia és essencial.

| Acció | Comanda | Explicació / Exemple |
| --- | --- | --- |
| Actualitzar la llista de repositoris | `sudo apt update` | Consulta els servidors per veure si hi ha paquets nous. |
| Actualitzar tots els paquets instal·lats | `sudo apt upgrade -y` | Instal·la les versions noves dels paquets existents. |
| Actualitzar completament el sistema | `sudo apt full-upgrade -y` | Fa una actualització completa (pot eliminar paquets obsolets). |
| Netejar paquets innecessaris | `sudo apt autoremove -y` | Elimina paquets antics no necessaris. |

* * *

🔹 **2\. Navegar pel sistema de fitxers**
-----------------------------------------

| Acció | Comanda | Explicació / Exemple |
| --- | --- | --- |
| Veure on estem | `pwd` | Mostra el directori actual. |
| Canviar de directori | `cd /etc/apache2` | Entra al directori especificat. |
| Tornar al directori anterior | `cd -` | Torna a l’últim directori visitat. |
| Tornar a la carpeta inicial (usuari) | `cd` | Va a `/home/usuari`. |

* * *

🔹 **3\. Llistar contingut de carpetes**
----------------------------------------

| Acció | Comanda | Exemple / Explicació |
| --- | --- | --- |
| Llistar fitxers | `ls` | Mostra els fitxers del directori actual. |
| Llistar amb detalls | `ls -l` | Mostra permisos, propietaris, mida i data. |
| Llistar també fitxers ocults | `ls -la` | Inclou fitxers que comencen amb “.” (com `.htaccess`). |
| Ordenar per data | `ls -lt` | Els més recents al principi. |

* * *

🔹 **4\. Crear i eliminar fitxers o carpetes**
----------------------------------------------

| Acció | Comanda | Exemple |
| --- | --- | --- |
| Crear carpeta | `mkdir /var/www/prova1` | Crea el directori `prova1`. |
| Crear fitxer buit | `touch /var/www/html/index.html` | Crea un fitxer nou si no existeix. |
| Eliminar fitxer | `rm fitxer.txt` | Elimina un fitxer. |
| Eliminar carpeta buida | `rmdir carpeta` | Només si està buida. |
| Eliminar carpeta amb contingut | `rm -r carpeta` | Elimina tot el contingut. (⚠️ Compte!) |

* * *

🔹 **5\. Veure contingut d’un fitxer**
--------------------------------------

| Comanda | Explicació | Exemple |
| --- | --- | --- |
| `cat fitxer` | Mostra tot el contingut del fitxer. | `cat /etc/hosts` |
| `more fitxer` | Mostra per pàgines (avança amb espai). | `more /etc/apache2/apache2.conf` |
| `less fitxer` | Com `more`, però permet moure’m endavant/enrere. | `less /etc/apache2/ports.conf` |
| `head fitxer` | Mostra les primeres 10 línies. | `head /var/log/apache2/error.log` |
| `tail fitxer` | Mostra les últimes 10 línies. | `tail /var/log/apache2/access.log` |
| `tail -f fitxer` | Mostra en temps real el final del fitxer (molt útil per veure logs). | `tail -f /var/log/apache2/error.log` |

* * *

🔹 **6\. Editar fitxers de configuració**
-----------------------------------------

| Editor | Comanda | Exemple |
| --- | --- | --- |
| **nano** (fàcil i per defecte) | `sudo nano /etc/apache2/sites-available/000-default.conf` | Editem configuracions d’Apache. |
| **Ctrl + O** → Guardar, **Ctrl + X** → Sortir | — | — |

* * *

🔹 **7\. Cercar arxius i continguts**
-------------------------------------

| Acció | Comanda | Exemple |
| --- | --- | --- |
| Cercar fitxer pel nom | `find /etc/apache2 -name "ports.conf"` | Busca un fitxer concret dins `/etc/apache2`. |
| Cercar fitxer a tot el sistema | `sudo find / -name "php.ini"` | Busca qualsevol `php.ini`. |
| Cercar text dins fitxers | `grep -rin "DocumentRoot" /etc/apache2/` | Mostra línies que contenen la paraula buscada. |
| Cercar amb _locate_ (més ràpid) | `locate 000-default.conf` | Usa una base de dades prèvia (`sudo updatedb` per actualitzar). |

* * *

🔹 **8\. Comprovar instal·lació i paquets**
-------------------------------------------

| Acció | Comanda | Exemple / Explicació |
| --- | --- | --- |
| Cercar paquet instal·lat | \`dpkg -l | grep apache2\` |
| Veure si un paquet està disponible | `apt-cache search php` | Busca paquets relacionats amb PHP. |
| Veure informació d’un paquet | `apt show apache2` | Mostra versió, dependències, etc. |

* * *

🔹 **9\. Gestionar serveis**
----------------------------

| Acció | Comanda |
| --- | --- |
| Veure estat d’Apache | `sudo systemctl status apache2` |
| Reiniciar Apache | `sudo systemctl restart apache2` |
| Tornar a carregar la configuració | `sudo systemctl reload apache2` |
| Aturar Apache | `sudo systemctl stop apache2` |
| Activar arrencada automàtica | `sudo systemctl enable apache2` |
| Desactivar arrencada automàtica | `sudo systemctl disable apache2` |

* * *

🔹 **10\. Activar / desactivar mòduls, llocs i configuracions d’Apache**
------------------------------------------------------------------------

| Acció | Comanda | Exemple |
| --- | --- | --- |
| Activar un **site** | `sudo a2ensite nomdelarxiu.conf` | `sudo a2ensite prova.conf` |
| Desactivar un **site** | `sudo a2dissite nomdelarxiu.conf` | `sudo a2dissite 000-default.conf` |
| Activar un **mòdul** | `sudo a2enmod rewrite` | Per exemple, habilitar “mod\_rewrite”. |
| Desactivar un **mòdul** | `sudo a2dismod rewrite` | Deshabilita el mòdul. |
| Activar config extra | `sudo a2enconf security` | Activa configuracions de `/etc/apache2/conf-available`. |
| Desactivar config extra | `sudo a2disconf security` | — |
| Després de qualsevol canvi | `sudo systemctl reload apache2` | Aplica els canvis sense reiniciar completament. |

* * *

🔹 **11\. Altres comandes útils**
---------------------------------

| Acció | Comanda | Explicació |
| --- | --- | --- |
| Veure IP del servidor | `ip a` o `hostname -I` | Mostra adreces IP de totes les interfícies. |
| Veure usuaris connectats | `who` o `w` | Mostra sessions actives. |
| Veure ús del disc | `df -h` | Mostra espai lliure. |
| Veure mida d’una carpeta | `du -sh /var/www/html` | Mostra l’espai ocupat. |
| Monitoritzar processos | `top` o `htop` | Mostra ús de CPU/memòria. |
| Provar connexió a un servidor | `ping ip` o `ping domini.cat` | Comprova si hi ha connexió. |

* * *

📘 **Resum essencial per configuracions d’Apache**
--------------------------------------------------

| Tasca | Comanda resum |
| --- | --- |
| Editar fitxer VirtualHost | `sudo nano /etc/apache2/sites-available/misite.conf` |
| Activar VirtualHost | `sudo a2ensite misite.conf` |
| Activar mòdul PHP | `sudo a2enmod php8.3` |
| Comprovar sintaxi d’Apache | `sudo apache2ctl configtest` |
| Reiniciar servei | `sudo systemctl reload apache2` |

* * *

Vols que et prepari una **taula resum imprimible** (tipus fitxa de comandes bàsiques de servidor Linux + Apache) per repartir als alumnes o tenir com guia ràpida?

## Response:
Perfecte 👌 — et deixo una explicació **completa, clara i didàctica** dels **contextos de configuració d’Apache2**, els **fitxers on s’apliquen**, els **valors per defecte** i les **configuracions més habituals**.

Això t’ajudarà tant per **entendre la jerarquia de configuració** com per **saber on posar cada directiva segons el context correcte**.

* * *

🧩 **Contextos de configuració a Apache2**
==========================================

Apache permet configurar el comportament del servidor en diferents nivells, anomenats **contextos**.  
Cada context defineix **on** s’aplica una directiva (a tot el servidor, a un lloc concret, a un directori, etc.) i en **quin fitxer** s’ha de col·locar.

Els principals contextos són:

* * *

🔹 **1️⃣ Server Config**
------------------------

### 📍 **Què és**

És el **nivell global del servidor Apache**.  
Les directives definides aquí afecten **tots els VirtualHosts i tots els llocs web** servits per Apache.

### 📁 **Fitxers de configuració**

*   `/etc/apache2/apache2.conf` → fitxer principal de configuració.
*   `/etc/apache2/ports.conf` → defineix els ports d’escolta (`Listen 80`, `Listen 443`).
*   També poden aparèixer al final d’altres fitxers de configuració global.

### ⚙️ **Exemples de directives habituals**

```apache
ServerRoot "/etc/apache2"
PidFile /var/run/apache2/apache2.pid
Timeout 300
KeepAlive On
MaxKeepAliveRequests 100
Listen 80
ServerName ipDelServidor.cat
```

### 🔧 **Valor per defecte**

*   Apache escolta al port **80** (`Listen 80`).
*   No hi ha `ServerName` definit (pot donar un _warning_ fins que s’afegeix).
*   El `DocumentRoot` per defecte és `/var/www/html`.

### 🧠 **Quan utilitzar-lo**

Quan vols definir paràmetres **globals del servidor**, com:

*   Ports d’escolta (`Listen`)
*   Nom del servidor (`ServerName`)
*   Mòduls carregats
*   Política d’accés per defecte
*   Límits o opcions de rendiment

* * *

🔹 **2️⃣ VirtualHost**
----------------------

### 📍 **Què és**

Permet definir **llocs web independents** (hosts virtuals) dins d’un mateix servidor Apache.  
Cada VirtualHost pot tenir:

*   El seu domini propi (`ServerName`)
*   El seu directori arrel (`DocumentRoot`)
*   Les seves pròpies opcions, errors i redireccions

### 📁 **Fitxers de configuració**

*   `/etc/apache2/sites-available/` → conté els llocs web definits però **no activats**
*   `/etc/apache2/sites-enabled/` → conté enllaços simbòlics als llocs activats
*   Fitxer per defecte: `/etc/apache2/sites-available/000-default.conf`

Per activar o desactivar un lloc:

```bash
sudo a2ensite nomdelLloc.conf
sudo a2dissite nomdelLloc.conf
sudo systemctl reload apache2
```

### ⚙️ **Exemple**

```apache
<VirtualHost *:80>
    ServerName isardapache.cat
    DocumentRoot /var/www/isardapache
    DirectoryIndex index.html
    ErrorDocument 403 /errors/403.html
</VirtualHost>
```

### 🔧 **Valor per defecte**

*   Fitxer `000-default.conf`
    ```apache
    <VirtualHost *:80>
        DocumentRoot /var/www/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    ```
*   Port 80, sense `ServerName` definit
*   Arrel web: `/var/www/html`

### 🧠 **Quan utilitzar-lo**

Quan vols:

*   Servir **diversos dominis** o subdominis al mateix servidor
*   Assignar **arrels de directori diferents**
*   Definir **errors personalitzats** o redireccions per cada site

* * *

🔹 **3️⃣ Directory**
--------------------

### 📍 **Què és**

Defineix **directives aplicables a un directori concret** del sistema de fitxers i als seus subdirectoris.

### 📁 **Fitxers de configuració**

Aquest context apareix normalment dins:

*   `/etc/apache2/apache2.conf`
*   o dins un fitxer `.conf` d’un VirtualHost, com ara `/etc/apache2/sites-available/misite.conf`

### ⚙️ **Exemple**

```apache
<Directory /var/www/html/prova1>
    Options Indexes FollowSymLinks
    AllowOverride None
    Require all granted
</Directory>
```

### 🔧 **Valors per defecte**

*   A `/etc/apache2/apache2.conf` hi ha una secció com aquesta:
    ```apache
    <Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>
    ```

### 🧠 **Quan utilitzar-lo**

Quan vols controlar:

*   Quines opcions estan disponibles (`Options`)
*   Si els `.htaccess` poden sobreescriure configuracions (`AllowOverride`)
*   Qui pot accedir (`Require`)
*   Llistat de directoris (`Indexes`)

### ⚙️ **Directives habituals**

| Directiva | Funció | Exemple |
| --- | --- | --- |
| `Options` | Defineix permisos (CGI, Indexes, Includes...) | `Options Indexes FollowSymLinks` |
| `AllowOverride` | Permet o no `.htaccess` | `AllowOverride None` |
| `Require` | Controla l’accés | `Require all granted` o `Require ip 192.168.1` |

* * *

🔹 **4️⃣ .htaccess**
--------------------

### 📍 **Què és**

Fitxer de configuració **local** que pot afegir-se en qualsevol directori del lloc web.  
Permet als usuaris modificar algunes directives **sense accedir als fitxers globals** d’Apache.

### ⚠️ **Important**

Perquè `.htaccess` tingui efecte, la directiva `AllowOverride` del `Directory` ha d’estar configurada correctament.

```apache
<Directory /var/www/html>
    AllowOverride All
</Directory>
```

### ⚙️ **Exemple de .htaccess**

```apache
# Redirecció
Redirect /antic /nou

# Pàgina per defecte
DirectoryIndex benvinguda.html

# Protegir directori
Require all denied
```

### 🔧 **Ubicació**

El `.htaccess` es guarda **dins del directori** al qual s’aplica, per exemple:

```
/var/www/html/.htaccess
```

### 🧠 **Quan utilitzar-lo**

*   Quan **no tens accés** a la configuració global (per ex., hosting compartit)
*   Quan vols que **subdirectoris** tinguin configuracions diferents (redireccions, URL rewriting, etc.)

### ❗ **Desavantatges**

*   Apache ha de llegir el fitxer `.htaccess` a cada petició → **pot afectar el rendiment**
*   Millor utilitzar **<Directory>** en configuracions globals si tens permisos

* * *

📘 **Resum comparatiu**
=======================

| Context | Afecta a | Fitxer / Ubicació | Exemple típic de directiva | Permet `.htaccess`? |
| --- | --- | --- | --- | --- |
| **Server Config** | Tot el servidor | `/etc/apache2/apache2.conf`, `ports.conf` | `Listen`, `ServerName` | ❌ No |
| **VirtualHost** | Un domini o site concret | `/etc/apache2/sites-available/*.conf` | `DocumentRoot`, `ErrorDocument`, `Redirect` | ✅ (si AllowOverride ho permet) |
| **Directory** | Un directori del sistema de fitxers | Dins `.conf` (apache2.conf o VirtualHost) | `Options`, `AllowOverride`, `Require` | ✅ (si AllowOverride ≠ None) |
| **.htaccess** | El directori i subdirectoris on està ubicat | Fitxer `.htaccess` dins el lloc web | `Redirect`, `DirectoryIndex`, `RewriteRule` | — |

* * *

Vols que et prepari aquest mateix contingut en **format esquema visual o fitxa Markdown per MkDocs**, amb exemples destacats i quadres de colors per a estudi? (ideal per aula o apunt digital).

## Response:
Perfecte 👍 Aquí tens una **explicació completa i estructurada** de les **directives d’Apache2**, amb exemples clars i el **context** on s’apliquen habitualment.

* * *

🧩 1️⃣ Què són les directives d’Apache?
---------------------------------------

Les **directives d’Apache** són **instruccions de configuració** que defineixen com el servidor web Apache gestiona:

*   Les peticions HTTP,
*   Els fitxers i directoris,
*   Els permisos,
*   Els errors,
*   I el comportament dels llocs web allotjats.

👉 Cada directiva es pot definir en diferents **contextos** segons l’abast que es vulgui donar a la configuració.

* * *

🗂️ 2️⃣ Contextos principals d’Apache
-------------------------------------

| Context | Descripció | Fitxers on es defineix | Exemple típic |
| --- | --- | --- | --- |
| **Server config** | Configuració global del servidor (afecta tots els VirtualHost). | `/etc/apache2/apache2.conf` o fitxers de `/etc/apache2/conf-available/` | Port d’escolta, mòduls, permisos globals. |
| **VirtualHost** | Configuració per a cada lloc web o domini. | `/etc/apache2/sites-available/<nom>.conf` | Domini, arrel del lloc, logs, redireccions. |
| **Directory** | Configuració per a un directori concret del sistema. | Dins `apache2.conf` o dins un fitxer VirtualHost | Permisos, index, opcions, restriccions. |
| **.htaccess** | Fitxer ocult dins d’un directori web. Permet modificar opcions locals **sense tocar la configuració global**. | Dins del directori web (`/var/www/html/...`) | Redireccions, errors personalitzats, permisos. |

* * *

⚙️ 3️⃣ Directives bàsiques i més habituals
------------------------------------------

### 🖥️ a) `ServerName` i `ServerAlias`

*   **Què fa:** Defineix el nom de domini principal i els noms alternatius.
*   **Context:** `VirtualHost`
*   **Exemple:**
    ```apache
    <VirtualHost *:80>
        ServerName isardapache.cat
        ServerAlias www.isardapache.cat
        DocumentRoot /var/www/isardapache
    </VirtualHost>
    ```

* * *

### 📂 b) `DocumentRoot`

*   **Què fa:** Indica el directori arrel on Apache buscarà els fitxers del lloc web.
*   **Context:** `VirtualHost`
*   **Exemple:**
    ```apache
    DocumentRoot /var/www/html
    ```

* * *

### 🧱 c) `DirectoryIndex`

*   **Què fa:** Defineix la pàgina per defecte si no s’especifica cap fitxer a la URL.
*   **Context:** `Directory`, `.htaccess`, `VirtualHost`
*   **Exemple:**
    ```apache
    DirectoryIndex index.html index.php
    ```

* * *

### 🧩 d) `ErrorDocument`

*   **Què fa:** Personalitza la resposta que mostra Apache en errors (403, 404, etc.).
*   **Context:** `VirtualHost`, `Directory`, `.htaccess`
*   **Exemple:**
    ```apache
    ErrorDocument 403 /errors/403.html
    ErrorDocument 404 /errors/404.html
    ```

* * *

### 🔄 e) `Redirect`

*   **Què fa:** Redirigeix una URL a una altra.
*   **Context:** `VirtualHost`, `Directory`, `.htaccess`
*   **Exemple:**
    ```apache
    Redirect /antic http://ipdelservidor.cat/nou
    Redirect permanent /nou https://nouweb.cat
    ```

* * *

### 🧭 f) `Alias`

*   **Què fa:** Assigna un camí de l’URL a un directori físic diferent de `DocumentRoot`.
*   **Context:** `Server config`, `VirtualHost`
*   **Exemple:**
    ```apache
    Alias /prova3 /var/www/prova3
    <Directory /var/www/prova3>
        Options -Indexes
        Require all granted
    </Directory>
    ```

* * *

### 🔒 g) `Require`

*   **Què fa:** Controla l’accés als fitxers segons IP, usuari, grup o autenticació.
*   **Context:** `Directory`, `.htaccess`
*   **Exemple:**
    ```apache
    <Directory /var/www/html/privat>
        Require ip 192.168.1.100
    </Directory>
    ```

* * *

### ⚙️ h) `Options`

*   **Què fa:** Defineix quines funcionalitats estan actives dins d’un directori.
*   **Context:** `Directory`, `.htaccess`
*   **Valors habituals:**
    *   `Indexes` → permet veure el llistat de fitxers
    *   `FollowSymLinks` → permet enllaços simbòlics
    *   `ExecCGI` → permet scripts CGI
    *   `None` → desactiva totes les opcions
*   **Exemple:**
    ```apache
    <Directory /var/www/html/public>
        Options +Indexes +FollowSymLinks
    </Directory>
    ```

* * *

### 📜 i) `AllowOverride`

*   **Què fa:** Indica si un `.htaccess` pot sobreescriure opcions del servidor.
*   **Context:** `Directory`
*   **Exemple:**
    ```apache
    <Directory /var/www/html>
        AllowOverride All
    </Directory>
    ```
    🔹 Sense això, `.htaccess` **no té efecte**.

* * *

### 🔊 j) `LogLevel` i `CustomLog`

*   **Què fan:** Controlen el nivell de detall i la ubicació dels logs.
*   **Context:** `Server config`, `VirtualHost`
*   **Exemple:**
    ```apache
    LogLevel warn
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    ```

* * *

🌍 4️⃣ Fitxers principals de configuració a Ubuntu
--------------------------------------------------

| Fitxer o carpeta | Funció |
| --- | --- |
| `/etc/apache2/apache2.conf` | Configuració global. |
| `/etc/apache2/sites-available/` | Fitxers dels VirtualHosts. |
| `/etc/apache2/sites-enabled/` | Enllaços als llocs actius. |
| `/etc/apache2/mods-available/` | Configuracions de mòduls disponibles. |
| `/etc/apache2/mods-enabled/` | Mòduls activats. |
| `/etc/apache2/conf-available/` | Configuracions generals addicionals. |
| `/var/www/html/` | Directori web per defecte. |

* * *

🧭 5️⃣ Exemple resum de configuració completa
---------------------------------------------

```apache
<VirtualHost *:80>
    ServerName isardapache.cat
    ServerAlias www.isardapache.cat
    DocumentRoot /var/www/isardapache

    DirectoryIndex index1.html

    <Directory /var/www/isardapache>
        Options -Indexes +FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorDocument 403 /errors/403.html
    LogLevel warn
    ErrorLog ${APACHE_LOG_DIR}/isard_error.log
    CustomLog ${APACHE_LOG_DIR}/isard_access.log combined
</VirtualHost>
```

* * *

🧠 6️⃣ Resum final
------------------

| Directiva | Funció principal | Context més habitual |
| --- | --- | --- |
| `ServerName`, `ServerAlias` | Defineixen dominis | VirtualHost |
| `DocumentRoot` | Arrel web | VirtualHost |
| `DirectoryIndex` | Fitxer per defecte | Directory / .htaccess |
| `ErrorDocument` | Personalitzar errors | VirtualHost |
| `Redirect`, `Alias` | Redireccions o mapes | VirtualHost |
| `Options`, `Require`, `AllowOverride` | Permisos i opcions d’accés | Directory |
| `LogLevel`, `CustomLog` | Registre d’errors i accessos | VirtualHost / global |

* * *

Vols que et prepare una **versió resumida en esquema visual (tipus fitxa de classe o resum d’examen)** amb exemples concrets per cada context (`ServerConfig`, `VirtualHost`, `Directory`, `.htaccess`)? Seria molt útil per imprimir o estudiar.



---
Powered by [ChatGPT Exporter](https://www.chatgptexporter.com)