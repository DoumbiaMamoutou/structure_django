# structure_django
```

# I- Comment installer django
#I-1 Intall Django mac os
##Setup 1
###Vérifier que python est installé

```
$ python3
```
```##Setup 2: créer un environnement virtuel```

```
$ python3 -m venv venv
```
##Setup 3: activer l'environnement virtuel

```
$ source venv/bin/activate
```
##Setup 4:Installer Django
```
$ pip3 install Django
```

##Setup 6:Création de notre projet

```
$ django-admin startproject myproject

```
```
myproject/
    bd.sqlite3        #Base de données par defaut
    manage.py         #manage.py va nous aider a lancer les commande
    myproject/        #application core
        __init__.py   #fichier init de python a ne pas supprimer
        settings.py   #fichier de configuration
        urls.py       #gestion de routage
        wsgi.py       #Utile pour le deploiement

```
##Setup 7: lancer le serveur django
```
$ cd myproject
$ python3 manage.py runserver
```

```

```
#settings.py projet
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': ['templates'],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static')
]
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, '../media_cdn')
STATIC_ROOT = os.path.join(BASE_DIR, '../static_cdn')
```
#urls.py projet
```
from django.contrib import admin
from django.urls import path,include
from django.conf.urls.static import static
from django.conf import settings

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('AppName.urls')),

]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root = settings.MEDIA_ROOT)
    urlpatterns += static(settings.STATIC_URL, document_root = settings.STATIC_ROOT)
```

# II- Model et Admin
## II-1 Models
#### ici nous allons profiter de l'ORM de django

### Models
```
statut = models.BooleanField(default=False)
   created_at = models.DateTimeField(auto_now_add=True)
   updated_at = models.DateTimeField(auto_now=True)
   
   
   post = models.ForeignKey(Post, on_delete=models.CASCADE,related_name="post_article", null=true)
   
   python manage.py makemigrations
   python manage.py migrate
   
   pip freeze
   pip freeze > requirements.txt
```
