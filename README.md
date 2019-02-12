======================
DJANGO OSCAR CATALOGUE
======================

Django Oscar Catalogue is a small packet of code extracted from Django Oscar,
to isolate the catalogue module independantly along with its dashboard.

Django Oscar Handles Products, Categories and its Attributes in one of the best approach,
which favors high amount of customization even from Dashboard. Also, it provides a basic
Dashboard to handle those products and associated things. django-oscar encapsulated all
those into a single module named 'oscar.apps.catalogue'.

Due to some Dependency with other modules inside django-oscar, Its module cannot be
isolated as it is. Django-Oscar-Catalogue filtered out these dependencies, and isolated
the module.

This retains the complete structure and interface with its parent package (Django Oscar),
so that, at any point of your project; you can simply unplug this module and install
django-oscar with minimum effort.


## README 
### Django-Oscar-Catalogue


Main Setting Dependancies are updated in  README.md
API Documentation for catalogue can be referred from official Documentation of django-oscar.


#### Packages.


Ensure these Python packages are added in your environment.

1) haystack

2) treebeard

3) sorl.thumbnail

4) django_tables2


#### SETTINGS FOR PACKAGE

Almost All Oscar Settings are added in *'oscar.default.\*'*
You can override them after importing these settings in your settings.py .

``get_core_apps()`` will include the following apps with your INSTALLED_APPS.


    OSCAR_CORE_APPS = [
        'oscar',
        'oscar.apps.catalogue',
        'oscar.apps.catalogue.reviews',
        'oscar.apps.dashboard',
        'oscar.apps.dashboard.catalogue',
        # 3rd-party apps that oscar depends on
        'haystack',
        'treebeard',
        'sorl.thumbnail',
        'django_tables2',
    ]

Django Oscar uses ``django.contrib.flatpages.middleware.FlatpageFallbackMiddleware``
to handle urls.

Oscar Guides Django uses 'OSCAR_MAIN_TEMPLATE_DIR' to search for templates.

Oscar-Catalogue uses 'oscar.template_loaders.OscarLoader' as template loader.

But when you switch to `django-oscar` package this can be removed.

    TEMPLATES['context_processors'].append('oscar.core.context_processors.metadata')
    TEMPLATES['loaders'].append('oscar.template_loaders.OscarLoader')
    
Oscar Guides Django uses 'HAYSTACK_CONNECTIONS' To establish Haystack for search. 

In your `settings.py`; append:

    from oscar.defaults import *
    from oscar import get_core_apps

    INSTALLED_APPS = [
    ...
    ...
    ] + get_core_apps()

    SITE_ID = 1
    OSCAR_MAIN_TEMPLATE_DIR = os.path.join(os.path.join(BASE_DIR), 'oscar', 'templates', 'oscar')
    TEMPLATES = [
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [],
            ...
            ...
            'APP_DIRS': False,
            'OPTIONS': {
            'context_processors': [
                ...
                ...
                'oscar.core.context_processors.metadata',
            ],
            'loaders':[
                    'django.template.loaders.app_directories.Loader',
                    ...
                    'oscar.template_loaders.OscarLoader',   # only to be used with oscar_catalogue not with oscar
                ],
            },
        },
    ]

    MIDDLEWARE = (
        ...
        'django.contrib.flatpages.middleware.FlatpageFallbackMiddleware',
    )

    HAYSTACK_CONNECTIONS = {
        'default': {
            'ENGINE': 'haystack.backends.simple_backend.SimpleEngine',
        },
    }

#### URLS FOR PACKAGE

Oscar-Catalogue uses these two urls to access catalogue of products and its dashboard.

    urls = [
            path('', self.catalogue_app.urls),
            path('dashboard/', self.dashboard_app.urls)
    ]


in your ``urls.py``; append:

    from...
    from oscar.app import application

    urlpatterns = [
        ...
        path('oscar/', include( application.urls[:2] )),
        ...
    ]

LICENSE is added in the "LICENSE" file.

We Call for contributions to make it efficient, up-to-date with django-oscar, and issue fixing

Pull a PR and Contributors List will be managed Soon. or else Raise an Issue to support us!


