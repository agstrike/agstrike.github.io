+++
title = "Dev Setup"
date =  2017-12-19T11:51:19+01:00
draft = false

[menu.main]
    name = "Dev Setup"
    parent = "Setup & Upgrade"
    weight = 2
+++

If you want to modify SilverStrike to adapt it to your usecase of you want to help in development,
this is the right place to look for information.

You should start by cloning the repository.
SilverStrike uses Git. You don't need to know very much about it to start.
If you don't know about it, I recommend searching the internet, there are numerous tutorials
and questions on stack overflow that will help you get started.

The only other prerequisite that you need is Python3.

This guide assumes you are cloning to `~/dev/silverstrike`.

The first step is to setup a virtual environement and install the required dependencies.
This is best done by just installing SilverStrike for development:

```
cd ~/dev/silverstrike
python3 -m venv demo/env
source demo/env/bin/activate
python setup.py develop
```

Before you run SilverStrike for the first time, you will need to setup a database and the first user account:

```
cd ~/dev/silverstrike/demo
source env/bin/activate
python manage.py migrate
python manage.py createsuperuser
```

You can then proceed to run the builtin development server:

```
cd ~/dev/silverstrike/demo
source env/bin/activate
python manage.py runserver
```

You should now be able to access Silverstrike over http://localhost:8000

Note that this server should only be used for development.
By default SilverStrike will only be accessible from the local machine.
So in theory you could use it for a local install, but it should never ever face the internet!
