# SIG 2 - Evaluation pratique 2024 - Docker

## Travail préparatoire

### Récupérer la dernière image de apache en exécutant les commandes suivantes

* Récupérer l'image

```
[INPUT]
docker pull httpd:alpine
```

```
[OUTPUT]
alpine: Pulling from library/httpd
4abcf2066143: Pull complete
5e13f4f5374d: Pull complete
333c1d8ec87c: Pull complete
4f4fb700ef54: Pull complete
58593e44a54d: Pull complete
608381599c68: Pull complete
d6e5ce613b31: Pull complete
Digest: sha256:6b242338c5c497fef59963d961e1f224262fc313482943cdf16b1875da26836f
Status: Downloaded newer image for httpd:alpine
docker.io/library/httpd:alpine
```

* Valider le résultat

```
[INPUT]
docker images
```

```
[OUTPUT]
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
httpd        alpine    43b6bf3450e2   12 days ago   61.6MB
```

<div style="page-break-after: always;"></div>

### Instancier le conteneur

Information technique : l'[image officielle](https://hub.docker.com/_/httpd) de Apache écoute par défaut le port 80.

* Lancer le conteneur en mappant le port local 80 avec le port 80 du conteneur

```
[INPUT]
docker run -p 80:80 httpd:alpine
```

```
[OUTPUT]
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
[Tue Apr 16 22:49:44.062977 2024] [mpm_event:notice] [pid 1:tid 140410165103368] AH00489: Apache/2.4.59 (Unix) configured -- resuming normal operations
[Tue Apr 16 22:49:44.063060 2024] [core:notice] [pid 1:tid 140410165103368] AH00094: Command line: 'httpd -D FOREGROUND'
172.17.0.1 - - [16/Apr/2024:22:50:17 +0000] "GET / HTTP/1.1" 200 45
172.17.0.1 - - [16/Apr/2024:22:50:18 +0000] "GET /favicon.ico HTTP/1.1" 404 196
```

* Valider la redirection de port et l'état du conteneur

```
[INPUT]
docker ps -a
```

```
[OUTPUT]
CONTAINER ID   IMAGE          COMMAND              CREATED              STATUS              PORTS                NAMES
55e4ba51b1a6   httpd:alpine   "httpd-foreground"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp   <name>
```

<div style="page-break-after: always;"></div>

### Afficher la page d'accueil de Apache

* Variante en ligne de commande

```
[INPUT]
curl localhost
```

```
[OUTPUT]
<html><body><h1>It works!</h1></body></html>
```

*** fin du document ***