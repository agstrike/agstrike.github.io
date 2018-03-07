+++
title = "Docker"
date =  2017-12-19T13:27:31+01:00
draft = false

[menu.main]
    name = "Docker"
    parent = "Setup & Upgrade"
+++

Docker images are provided under the name `simhnna/silverstrike`.
There are two tags:

* **latest** will always corrospond to the current release of SilverStrike.
* **dev** will match the master branch of SilverStrike.

I highly recommend to use the latest tag, as this is the one that has been tested.
You can use the dev tag if you just want to try it out.
You shouldn't use it in production, because I can't guarantee the stability of it.

If you just want to start quickly here is a docker-compose file that will get you started:

```
---
version: "3.2"
services:
  app:
    environment:
      - ALLOWED_HOSTS='*'
      - DATABASE_URL=postgres://silverstrike:secretpass@database/silverstrikedb
      - SECRET_KEY=PLprXpLzxemgLD57GPQQ84SBZdLVKFYg
    image: simhnna/silverstrike
    links:
      - database:database
    ports:
      - 8000:8000
  database:
    environment:
      POSTGRES_DB: silverstrikedb
      POSTGRES_USER: silverstrike
      POSTGRES_PASSWORD: secretpass
    image: postgres:10.3
    volumes:
      - ./silverstrikedb:/var/lib/postgresql/data
```

All docker related stuff can be found in https://github.com/agstrike/docker


I highly recommend changing the `SECRET_KEY`. The database credentials aren't that important, but it won't hurt changing them too.


After starting the containers, you will still need to create a user using the command line.
You can do this using the following command.
```
docker-compose exec app python manage.py createsuperuser
```
