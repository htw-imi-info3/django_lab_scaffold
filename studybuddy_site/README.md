## Part 0
Libraries Installieren: django u.a. 

   source .venv_studybuddy/bin/activate
   pip install -r requirements.txt
## Part 1

    django-admin startproject studybuddy-site
    cd studybuddy_site
    python manage.py startapp studybuddy_app

    python manage.py migrate
    python manage.py runserver

    python manage.py createsuperuser

## Part 2

    python manage.py makemigrations studybuddy_app
    python manage.py sqlmigrate studybuddy_app 0001
    python manage.py migrate

### Shell

    python manage.py shell

#### In the Shell:

    from studybuddy_app.models import *
    from django.utils import timezone

    User.objects.all()

    Meetup.objects.all()
    
    m = Meetup(title="zusammen lernen")
    m.start_date = timezone.now()
    m.save()
    m1 = Meetup(title="Mathe Lernen", start_time=timezone.now())
    m1.save()

    Meetup.objects.all()


    m2 = Meetup(title="Info3 Lernen", start_time=timezone.now() + datetime.timedelta(days=3))
    m2.save()
    m2.is_upcoming()

    Meetup.objects.filter(id=1)

    current_year = timezone.now().year
    Meetup.objects.filter(start_time__year=current_year)

    
    m = Meetup.objects.get(pk=3)

    from studybuddy_app.models import *
    from django.utils import timezone
    m2 = Meetup(title="Info2 Lernen", start_time=timezone.now() + datetime.timedelta(days=1))
    m2.save()
    m2.is_upcoming()

    current_month = timezone.now().month
    Meetup.objects.filter(start_time__month=current_month)


    q.choice_set.create(choice_text="Not much", votes=0)
    q.choice_set.all()
    q.choice_set.count()
    q.choice_set.filter(choice_text__startswith="Just hacking")
    
    Meetup.objects.all().filter(title__startswith="Info")

## ManyToMany

    from studybuddy_app.models import *
    from django.contrib.auth.models import User

    from django.contrib.auth import get_user_model
    get_user_model()
    --> <class 'django.contrib.auth.models.User'>
    
    from django.contrib.auth.models import User
    User.objects.all()

    from django.contrib.auth.models import User

## Fixtures


    python manage.py dumpdata auth.User --natural-foreign --format yaml > studybuddy_app/fixtures/user.yaml

    python manage.py dumpdata studybuddy_app.Meetup --natural-foreign --format yaml > studybuddy_app/fixtures/meetup.yaml
## Tests

The scaffold contains a couple of example tests cases: 

- unit tests using the django test libraries in tests/
- acceptance tests using selenium in tests_selenium

the selenium tests needs geckodriver!
## Authentication and Authorization
### Login/Authentication

#### login-logout tutorial

https://learndjango.com/tutorials/django-login-and-logout-tutorial

#### signup tutorial

https://learndjango.com/tutorials/django-signup-tutorial

####  password-reset 

omitted. can be done via admin app for now.

https://learndjango.com/tutorials/django-password-reset-tutorial

### Authorization

https://docs.djangoproject.com/en/4.2/topics/auth/