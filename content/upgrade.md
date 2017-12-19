+++
title = "Upgrade Instructions"
date =  2017-12-19T13:46:16+01:00
draft = false

[menu.main]
    name = "Upgrade Instructions"
    parent = "Setup & Upgrade"
+++

Assuming you have installed SilverStrike according to the [setup instructions]({{< relref "setup.md" >}}).

Preparation:  
```
cd /srv/webapps/silverstrike
source env/bin/activate
```
1. Grab the upgrade from pypi  
`pip install --upgrade silverstrike`
2. Apply migrations  
`python manage.py migrate`    
3. Collect static files  
`python manage.py collectstatic`
4. Tell uwsgi to restart  
`touch /etc/uwsgi/vassals/silverstrike.ini`