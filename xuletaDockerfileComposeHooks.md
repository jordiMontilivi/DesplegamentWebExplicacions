# Xuleta Dockerfile i Docker-comnpose amb gestio de Volums

## Crear una imatge de apache, crear un volum, aixecar un contenidor (escolta al port 80 i te aquest volum) i finalment copiar fitxers

si volem generar una imatge de docker per parts podem:

1. Crear imatge a partir del dockerhub oficial d'Apache
2. Copiar els fitxers de la web al contenidor
3. Declarar un volum per persistència (opcional)

```bash
docker pull httpd:latest

docker tag httpd:latest web

docker volume create anime-volume

docker run -d -p 80:80 --name web-anime -v anime-volume:/usr/local/apache2/htdocs/ web

docker cp ./anime/ web-anime:/usr/local/apache2/htdocs/
```

Pots crear un contenidor temporal només per veure el contingut:

```bash
docker run --rm -v anime-volume:/data alpine ls -l /data
```

Hauries de veure els fitxers que has copiat.

## Crear un Dockerfile per automatitzar la creació de la imatge

```Dockerfile
# Imatge base oficial d’Apache
FROM httpd:latest

# Establece el directorio base para cualquier comando posterior
WORKDIR /usr/local/apache2/htdocs

# Copia la web al directorio público de Apache
COPY ./game-warrior/ .

# Declarar el volumen para persistencia (volum anònim)
# Actualment no s’està utilitzant un volum dintre del dockerfile sinó des al docker-compose.yml
VOLUME ["/usr/local/apache2/htdocs"]

EXPOSE 80
```

Amb aquest Dockerfile podem crear la imatge amb:

```bash
docker build -t game-warrior:latest .
```

Si volem utilitzar un Dockerfile amb un nom diferent, podem fer:

```bash
docker build -t game-warrior:latest -f Dockerfile.custom .
```

Si volem crear el contenidor amb el volum anònim declarat al Dockerfile, podem fer:

```bash
docker run -d -p 80:80 --name web-game-warrior game-warrior:latest
```

Exemple de com veure el contingut del volum anònim:

```bash
docker run --rm -v game-warrior:/data alpine ls -l /data
```

Com podem veure el volum anonim creat

```bash
docker volume ls
```

docker volume ls
DRIVER VOLUME NAME
local 19f4c1c03bba81a603c03e7d03675e0ced6b6a0365ad043c4391755b67b92c63

## Crear un docker-compose.yml per automatitzar la creació del servei

```yaml
services:
  web: # Nom del servei
    build: # si no vols especificar res mes pots posar només -> build: .
      context: . # Directori on es troba el Dockerfile
      dockerfile: Dockerfile # Opcional si el nom es Dockerfile
    container_name: game-warrior # Nom del contenidor
    image: game-warrior:latest # Nom de la imatge
    restart: always # Política de reinici
    ports: # Mapeig de ports
      - "80:80"
    volumes: # Volums
      - game-warrior:/usr/local/apache2/htdocs/

volumes:
  game-warrior: # nom del volum
    name: game-warrior
```

Amb aquest docker-compose.yml podem aixecar el servei amb:

```bash
docker compose up -d
```

Per a asegurarnos que no ens done warnings amb la imatge podem fer un docker compose build abans de fer el up:

```bash
docker compose up -d --build
```

Si volem aixecar un compose personalitzat amb un altre nom de fitxer:

```bash
docker compose -f custom-compose.yml up -d --build
```

Per aturar el servei (eliminant contenidors i xarxes creades pel docker-compose.yml):

```bash
docker compose down
```

Per aturar el servei (eliminant contenidors, xarxes i volums creats pel docker-compose.yml):

```bash
docker compose down -v
```

Per aturar el servei (eliminant contenidors, xarxes, volums i imatges creades pel docker-compose.yml):

```bash
docker compose down --rmi all -v
```

Per veure els logs del servei:

```bash
docker compose logs -f
```

Per veure els serveis actius:

```bash
docker compose ps
```

Per veure els volums creats:

```bash
docker volume ls
```

Control de canvis i pujada a un repositori git amb githooks per automatitzar la pujada a un repositori remot (github, gitlab, etc)
hem de controlar en quin hook volem que s'executi l'script, en aquest cas volem que s'executi abans de fer un commit (pre-commit)
Els hooks es troben a la carpeta .git/hooks dins del repositori local, haurem de crear un fitxer anomenat pre-commit (sense extensió) i donar-li permisos d'execució.

Pero abans hem de inicialitzar el repositori git:

```bash
git init
git remote add origin <url_del_repositori_remot> # no cal ara de moment si treballem en local
```

Creem el fitxer .git/hooks/pre-commit i li donem permisos d'execució:

```bash
touch .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

El contingut del fitxer pre-commit pot ser el següent:

```bash
# docker compose -f docker-compose-algo.yml down --rmi all -v
docker rm -f game-warrior
docker volume rm game-warrior

# docker volume rm $(docker volume ls -q --filter name=web1_game-warrior)???
# Opcional: indica el fitxer docker-compose si és personalitzat
docker compose up --build -d

# # Captura l'estat de l'últim comandament
# status=$?

# if [ $status -ne 0 ]; then
#   echo "Error executant docker compose. Abortant push."
#   exit 1
# fi

# echo "Docker compose ha acabat correctament. Continuant amb el push."
# exit 0
```

Aquest script atura i elimina el contenidor i volum actuals (eliminem el volum per a poder copiar la nova informació), i després aixeca el servei amb docker compose amb la opció --build per assegurar-se que es construeix la imatge abans d'aixecar el servei.
