# Django_cheatcodes
self.note(Django)
MAY 2, 2015 | YASK123
{% load staticfiles %}{% load staticfiles %}This post is going to be more like a self note with code snippets which I usually need for basic setup of any django application.
This will be updated as I discover more.

Basic setup of application:

 

1. Static files

1
2
3
4
5
6
7
8
STATICFILES_DIRS = (
    os.path.join(BASE_DIR,'static'),
    )
TEMPLATE_DIRS = (
    os.path.join(BASE_DIR,'templates'),
    )
 
STATIC_URL = '/static/'
Now put the static files inside each app’s template/static/app_name folder.
Whenever django gets the request to render the specific template file , it will start searching in every directory (/template/static/app_name) .

Referring to static files from your template

1
{% load staticfiles %}</p>
2. Changing default database to mysql

Typical setup of creating entities

1
2
3
4
5
6
7
8
9
10
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'firstdb',
        'USER':'root',
        'PASSWORD':'password',
        'HOST':'localhost',
        'PORT':'3306',
    }
}
 

1. Many-One (with Questions column as foreign key)

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
from django.db import models
 
# Create your models here.
class Question(models.Model):
    text = models.CharField(max_length=200)
    date = models.DateTimeField('Date Published')
    def __str__(self):
        return self.text
 
class Choice(models.Model):
    question = models.ForeignKey(Question)
    text = models.CharField(max_length=500)
    votes = models.IntegerField(default=0)
    def __str__(self):
        return self.text
2. To display entities in database nicely from /admin

1
2
def __str__(self):
        return self.attribute_name
3. To register the model’s entities to enable their display from /admin

1
2
3
4
5
6
7
from django.contrib import admin
from polls.models import Question,Choice
# Register your models here.
 
admin.site.register(Question)
 
admin.site.register(Choice)
Typical way of URL mapping

To map urls from each specific application insdide Django’s project
inside main projects `urls.py`

1
url(r'^polls/',include('polls.urls')),
now inside app’s urls.py

1
2
3
from app_name import views
urlpattern=[
url(r'^about
,views.about),..]
[/code]

Basic operations on models

1
2
3
4
5
6
7
8
9
from app_name.models import Model_name
# get all attributes 
Model_name.objects.all()
#count them
(Model_name.objects.all().count())
#sort them
Model_name.objects.all().order_by('votes')
#add data 
Model_name.objects.create(attribute=value)
To contribute https://github.com/yask123/Django_cheatcodes [ I know it looks ugly there at present , I’ll format it soon ]
