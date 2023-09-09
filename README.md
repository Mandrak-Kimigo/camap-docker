# camap-docker

## Utiliser les containers

Les containers Camap sont utilisables en local.

Renseignez votre fichier hosts avec les valeurs:

```127.0.0.1 camap api.camap```

Puis ```docker compose up -d```

La configuration initiale se fait en accédant à https://camap/install

# Construction des containers depuis les sources

Script de construction des containers Camap

git clone https://github.com/Mandrak-Kimigo/camap-docker.git

## Prérequis

La présente documentation a été testée sur Debian 11

**Installer docker & docker-compose**

```apt-get install docker-buildx-plugin docker-ce docker-ce-cli docker-compose-plugin```

https://docs.docker.com/engine/install/debian/

## Configuration

### La configuration du container neko-camap se fait dans __config.xml__ de <DESTDIR>/camap-hx

```key``` doit avoir la même valeur que ```CAMAP_KEY``` dans camap-ts/.env
Cette clef est utilisée pour vérifier le hash des mots de passe des comptes Camap

```host``` nom d'hote sur serveur camap (1er terme de ```camap_api```)

```camap_api``` contient l'url du frontal Camap

```mapbox_server_token``` contient la clef pour les fonctions de géolocalisation, à créer sur mapbox.com (gratuit jusqu'à 100.000 requetes par mois)

### La configuration du container nest-camap se fait dans __.env__ de <DESTDIR>/camap-ts

```CAMAP_KEY``` doit avoir la même valeur que ```key``` dans camap-hx/config.xml
Cette clef est utilisée pour vérifier le hash des mots de passe des comptes Camap

```CAMAP_HOST``` contient l'url du frontal Camap (camap-hx)

```FRONT_URL``` contient l'url du serveur nest (camap-ts)

```FRONT_GRAPHQL_URL``` contient l'url de graphql (FRONT_URL/graphql)

La rubrique _MAIL_ doit être renseignée avec les informations de votre serveur de mail

## Installation Linux Debian

lancer
`build_camap_docker.sh <DESTDIR>`

pour une installation de Camap dans ```DESTDIR```

Renseigner le DNS ou votre fichier hosts avec les valeurs correspondante à la configuration.
Pour une installation en local:
```127.0.0.1 camap api.camap```

## Installation sous Windows

Installer docker desktop

Créer un répertoire Camap

Dans ce répertoire:

```git clone https://github.com/Mandrak-Kimigo/camap-hx.git```
```git clone https://github.com/Mandrak-Kimigo/camap-ts.git```
```git clone https://github.com/Mandrak-Kimigo/camap-docker.git```

Copier ensuite depuis camap/camap-docker/:
```*.Dockerfile``` dans ```camap```
```docker-compose.yml``` dans ```camap```
```.env``` dans ```camap/camap-ts```
```config.xml``` dans ```camap/camap-hx```

exécuter ```docker compose up -d --build```


L'installation est complètement dockerisée, l'édition des sources nécessite de relancer le build des containers

Après l'installation, remonter une sauvegarde via mysqlworkbench ou myloader ou créer le compte admin via https://camap/install

