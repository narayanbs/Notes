#### Prerequsite

**Create a python project as shown [[X02-Coding/Python|here]]**
#### Initialize Django project

```bash
django-admin startproject locallibrary
cd locallibrary
python manage.py startapp catalog
```
Register the app with the project by including it in locallibrary/settings.py
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # Add our new application
    'catalog.apps.CatalogConfig', #This object was created for us in /catalog/apps.py
]
```
Specify the database if any
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```
Update other project settings, if need be
```python
TIME_ZONE = "Asia/Kolkalta"
```
Hook up the urls to the app, by updating locallibrary/urls.py
```python
from django.contrib import admin
from django.urls import path
from django.urls import include
from django.conf import settings
from django.views.generic import RedirectView
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('catalog/', include('catalog.urls')),
]

#Add URL maps to redirect the base URL to our application
urlpatterns += [
    path('', RedirectView.as_view(url='catalog/', permanent=True)),
]

# Use static() to add URL mapping to serve static files during development (only)

urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```
As a final step create a urls.py inside catalog and add the following urlpatterns
```python
from django.urls import path
from . import views

urlpatterns = [

]
```
Run the database migrations
```bash
python3 manage.py makemigrations
python3 manage.py migrate
```
Finally, run the server at http://localhost:8000/
```bash
python manage.py runserver 
```