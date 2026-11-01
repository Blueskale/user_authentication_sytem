# Django User Authentication System

![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-4.2%20LTS-092E20?logo=django&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?logo=sqlite&logoColor=white)
![crispy-forms](https://img.shields.io/badge/django--crispy--forms-1.14-5c6bc0)

A complete user authentication flow built on Django's built-in `auth` framework: registration, login and logout, and a profile page with an avatar, plus a small blog app that shows how authenticated content fits in. The project was written while learning Django and is verified to run on **Django 4.2 LTS**.

## Features

- Registration form that extends `UserCreationForm` with a required email field
- Login and logout through Django's class-based `LoginView` and `LogoutView` with custom templates
- Profile page (login required) showing the username, email and profile picture
- `Profile` model with an image field, created automatically for every new user via `post_save` signals
- Forms rendered with django-crispy-forms (Bootstrap 4 template pack)
- Success messages after registration using the messages framework
- Blog app with a `Post` model (title, content, timestamp, author), a home page listing posts and an about page
- Media uploads served in development, with `default.jpg` used until a picture is uploaded

## Tech stack

Python 3 · Django 4.2 · django-crispy-forms 1.14 · Pillow · SQLite · HTML, CSS and JavaScript templates

## Project structure

```
django_project/
├── manage.py
├── django_project/     # settings, root URL configuration, WSGI entry point
├── blog/               # Post model, home/about views, base template, static assets
├── users/              # Profile model, registration form, signals, auth templates
├── media/              # uploaded profile pictures (profile_pics/) and default.jpg
└── db.sqlite3          # development database
```

## Getting started

```bash
git clone https://github.com/Blueskale/user_authentication_sytem.git
cd user_authentication_sytem
python3 -m venv venv && source venv/bin/activate     # Windows: venv\Scripts\activate
pip install -r requirements.txt
cd django_project
python manage.py migrate
python manage.py createsuperuser                     # optional, for /admin/
python manage.py runserver
```

Open http://127.0.0.1:8000/ and use **Register** to create an account, then log in and visit `/profile/`.

## URL map

| Path | View | Notes |
|---|---|---|
| `/` | `blog.views.home` | Lists all posts |
| `/about/` | `blog.views.about` | Static about page |
| `/register/` | `users.views.register` | Creates the account and redirects to login |
| `/login/` | `LoginView` | Redirects to the blog home after login |
| `/logout/` | `LogoutView` | Shows the logout template |
| `/profile/` | `users.views.profile` | Login required |
| `/admin/` | Django admin | Manage users, profiles and posts |

## Configuration

Settings live in `django_project/django_project/settings.py`:

- `LOGIN_URL = 'login'` and `LOGIN_REDIRECT_URL = 'blog-home'`
- `MEDIA_ROOT` / `MEDIA_URL` for uploads; Django serves them only while `DEBUG = True`
- `CRISPY_TEMPLATE_PACK = 'bootstrap4'`
- `SECRET_KEY` and `DEBUG = True` are development values. Load them from environment variables before deploying.

## Known limitations and next steps

- Profile editing (changing username, email or picture) is not implemented yet; the template has a placeholder for the form
- No automated tests yet
- Navigation links in the base template are placeholders
