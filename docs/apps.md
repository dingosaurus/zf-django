# Aplikace


```
Rozdělení do aplikací ok?
 
APPS_DIR v base settings - funguje, ale po zanoření asi není úplně správně použitý
Stejně tak STATIC_ROOT a MEDIA_ROOT .. Potřeba vysvětlit.
Collectstatic
```

---


## Struktura

```
any_app_name            # obal aplikace, hlavní složka, můžu být nazvána celkem libovolně
    app_name            # název celého projektu - bude následně v každém importu
        app_1           # aplikace 1
        app_1           # aplikace 2
        contrib         # místo pro další aplikace, pokud jich je velké množství
        common          # společné třídy, utility
        settings        # settings aplikace  
        __init__.py  
        urls.py  
        wsgi.py
    docs                # dokumentace, pokud je třeba ji mít v aplikaci
    media               # MEDIA_ROOT
    requirements        # requirements.txt, ...
    provisioning        # pokud je třeba pro nasazování
    static              # STATIC_ROOT
    manage.py           # je třeba mít podchycenou strukturu pro DJANGO_SETTINGS_MODULE
    MANIFEST.in         # build aplikace
    pytest.ini          # pytest
    setup.cfg           # build aplikace
    setup.py            # build aplikace
```

* Strukturu projektu je možno vygenerovat pomocí `manage.py startproject`.
* Každou aplikaci projektu je možno vygenerovat pomocí `manage.py startapp`.
* Možnost vygenerovat strukturu projektu pomocí cookiecutteru - např. [https://github.com/pydanny/cookiecutter-django]()
* Následně lze podle libosti zanořit

`STATIC_ROOT` 
- slouží jako úložiště pro statické soubory - js, css, jpg, ...
- V případě, že se použivá úložiště jako je např. AWS S3, tak určuje cestu na tomto úložišti.
- Dá se nastavit absolutně i __relativně__. 

`MEDIA_ROOT` 
- slouží jako úložiště pro dynamicky nahrané soubory - dokumenty, obrázky, ... == uživatelský obsah.
- Podobně jako `STATIC_ROOT`.

---


`settings/base.py`

```python
INSTALLED_APPS = [
    ...
    'app_name.app_1.App1Config',
    ...
]
```


`app_1/apps.py`

```python
from django.apps import AppConfig

class App1Config(AppConfig):
    name = 'app_name.app_1'
    
    def ready(self):
        from app_name.app_1.signals import *
    
```

--- 

[https://docs.djangoproject.com/en/3.2/ref/applications/]()

## Settings

```
settings
    base.py
    production.py
    localhost.py
    local.py
```

Používat [https://github.com/henriquebastos/python-decouple]() pro načtení dat z env proměnných



```python
# production.py

from .base import *
...
```

```python
# localhost.py

from .base import *
...
try:
    from .local import *
except ImportError:
    pass
```