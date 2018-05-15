# Docker

## Základy

### Termíny
- **Image:** zbuilděná service
- **Container:** běžící service (runtime instance)
- **Dockerfile:** Dokument obsahující příkazy, které bychom psali manuálně, kdybychom chtěli buildovat image.
- **Compose:** Nástoj pomocí kterého můžeme konfigurovat více-containerové aplikace pomocí jednoho souboru.
Další
- **Node (v kontextu dockeru):** uzel - stroj na kterém běží instance Docker Engine ve Swarm módu
- **Cluster:**

### Docker Compose

Docker compose umožňuje nastavit jednotlivé služby pomocí YAML souboru a jejich následné spuštění pomocí jednoho příkazu.

Proces používání Compose se skládá ze tří částí:
1. Definujeme Dockerfile jednotlivých služeb.
2. Definujeme služby, které tvoří naši aplikaci v docker-compose.yml.
3. Zavoláme docker-compose up (tim spustíme celou aplikaci)

[Compose file ref](https://docs.docker.com/compose/compose-file/) <br>
[Compose file overview](https://github.com/docker/docker.github.io/blob/master/compose/overview.md#only-recreate-containers-that-have-changed)

#### Build
Při změně v Dockerfile je potřeba udělat build.
```bash
docker-compose build
```

#### Spuštění

```bash
docker-compose up
```

Otevře interaktivní mód a loguje změny v containerech včetně zavádění.
Jedna z možností pro vývoj asi bude spustit si `docker-compose up -d` pro spuštění aplikace na pozadí. Pro následné logování by potom šlo logovat změny z konkrétních containerů pomocí `docker log` (zatím nevyzkoušeno).

Příkazy:
- `docker-compose up`
- `docker-compose up -d` spustí celou službu na pozadí
- `docker-compose rm` vymaže data - volumes atd.

### Volumes
(Překlad: obsah, kapacita, svazek)

- prostě místo na disku
- „přetrvávající - stálá“ data
- mohou být sdílena více containery

### Networks

### Debugging

- `docker ps` List běžících containerů
- `docker ps -a` List všech containerů
- `docker ps -a -q` List IDs všech containerů
- `docker exec CONTAINER PŘÍKAZ` Zavolá příkaz v containeru
- `docker exec -it CONTAINER` Zavolá příkaz v interaktivním módu
- `docker exec -it CONTAINER bash` Otevře bash
- `docker exec -it CONTAINER ash` Otevře ash shell (frontend)
- `docker-compose logs -f --tail=10` logování
- `docker-compose logs CONTAINER` logování konkrétního containeru
- `docker cp CONTAINER:SRC_PATH DEST_PATH` kopie souboru z containeru na hosta


### Run
docker run

Publish or expose port
-p HOST:CONTAINER (publish or expose port)

Inject enviroment variables from .env file
--env-file PATH

Příklad:
`docker run -p 80:3000`
Je to samé jako `docker run -p 127.0.0.1:80:3000 --env-file core.env`



### Build the project

If you want to run your services in the background, you can pass the -d flag (for “detached” mode) to docker-compose up and use docker-compose ps to see what is currently running:

Now, run docker-compose up -d from your project directory.

This runs docker-compose up in detached mode, pulls the needed images, and starts the wordpress and database containers, as shown in the example below.

### Vytvoření samostatného image
Go to service root
```bash
cd SERVICE-FOLDER
```

Build
```bash
docker build -t feedu:version .
```

Run
```bash
docker run --rm -p 3000:3000 fakinfeedu:version
```


### Čištění
!!! Bacha na volumes :D (databáze, obrázky atd.)

- `docker-compose rm` vymaže
- `docker [kill,rm,stop] $(docker ps -a -q)` Vypne, smaže, stopne všechny containery.
- `docker [image/container/volume] rm [id]`
- `docker [image/container/volume] prune`
- `docker system prune` Vymaže vše
- `docker system prune -af` Prune As Fuck!
