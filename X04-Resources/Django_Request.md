When request arrives, django looks at ROOT_URLCONF in settings.py and obtains the module 
containing the urlpatterns.
for ex:
```bash
ROOT_URLCONF = "locallibrary.urls"
```
It gets the urlpatterns and iterates through all the `django.urls.path()` and 
`django.url.re_path()` instances and stops at the first one that matches the requested 
URL., matching against path_info 

```bash
for path in root_conf.urlpatterns:
	p = path()
	if p.url.matches(request.url):
	......
	else:
		raise Error	
```

```bash
for repath in root_conf.urlpatterns:
	r = re_path()
	if r.regex.matches(request.url):
	....
	else
		raise Error
```

```bash
	urlpatterns = [
    path('articles/2003/', views.special_case_2003),
    path('articles/<int:year>/', views.year_archive),
    path('articles/<int:year>/<int:month>/', views.month_archive),
    path('articles/<int:year>/<int:month>/<slug:slug>/', views.article_detail),
	]
```

<int:year> -->  int is a converter and year is the name of the variable
	
if request is `/articles/2003/` then views.special_case_2003(request, 2003) is invoked.
if request is `/articles/2005/` then 	views.year_archive(request, year=2005) is 
invoked. 

if request is `/articles/2003/03/building-a-django-site/` then
`views.article_detail(request, year=2003, month=3, slug="building-a-django-site")`.

```bash
urlpatterns = [
    path('articles/2003/', views.special_case_2003),
    re_path(r'^articles/(?P<year>[0-9]{4})/$', views.year_archive),
    re_path(r'^articles/(?P<year>[0-9]{4})/(?P<month>[0-9]{2})/$', views.month_archive),
    re_path(r'^articles/(?P<year>[0-9]{4})/(?P<month>[0-9]{2})/(?P<slug>[\w-]+)/$', 
views.article_detail),
```

