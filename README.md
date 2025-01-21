# Django Extended User Profile

A Django project that allows registered users to edit their profiles outside the admin panel. This project is built using **Django** and **Bootstrap 5** to provide a smooth and user-friendly experience.

- 👉 **Live Demo**: [Django Extended User Profile](https://django-user-profile.appseed-srv1.com/)
- 👉 **Developer**: [Salah Saeed](https://github.com/salahsaeed19)

<br />

---

## Features

- **Profile Management**: Users can edit their personal information such as name, email, profile picture, and more.
- **User-Friendly Interface**: Designed using **Bootstrap 5** for a modern and responsive user experience.
- **User Authentication**: Users can register, log in, and manage their profiles easily.

<br />

## About Me

Hello! I'm **Salah Saeed**, a passionate developer with experience in building web applications using Django, Python, and modern front-end technologies. This project is part of my portfolio to showcase my skills in web development and user management systems.

- **GitHub**: [salahsaeed19](https://github.com/salahsaeed19)
- **Email**: [salahsaef40@gmail.com](mailto:salahsaef40@gmail.com)
- **Website**: [RCM Engineering](https://rcm-eng.com/)

<br />

---

## How to Use the Project

Follow these steps to set up and run the project locally:

```bash
# Clone the repository
$ git clone https://github.com/salahsaeed19/django-extended-user-profile.git
$ cd django-extended-user-profile

# Create a virtual environment (Unix-based systems)
$ virtualenv env
$ source env/bin/activate

# Create a virtual environment (Windows-based systems)
$ virtualenv env
$ .\env\Scripts\activate

# Install dependencies
$ pip install -r requirements.txt

# Apply database migrations
$ python manage.py makemigrations
$ python manage.py migrate

# Run the development server
$ python manage.py runserver

# Access the app in your browser: http://127.0.0.1:8000/
```

<br />

---

## Project Structure

The project is organized as follows:

```bash
< PROJECT ROOT >
   |
   |-- core/                               # Core application settings and configurations
   |    |-- settings.py                    # Django settings
   |    |-- static/                        # Static files (CSS, JS, images)
   |    |-- templates/                     # HTML templates
   |         |
   |         |-- includes/                 # Reusable HTML components
   |         |-- layouts/                  # Base templates
   |         |-- accounts/                 # Authentication templates
   |         |
   |      index.html                       # Default homepage
   |       *.html                          # Other HTML pages
   |
   |-- authentication/                     # Handles user authentication (login, register)
   |    |-- urls.py                        # Authentication routes
   |    |-- forms.py                       # Authentication forms
   |
   |-- customers/                          # Handles user profile management
   |    |-- models.py                      # Profile model
   |    |-- forms.py                       # Profile forms
   |    |-- views.py                       # Profile views
   |    |-- urls.py                        # Profile routes
   |
   |-- requirements.txt                    # Project dependencies
   |-- manage.py                           # Django management script
   |
   |-- ************************************************************************
```

<br />

---

## Key Features Implementation

### Profile Management

The project includes a `customers` app that allows users to manage their profiles. Key components include:

- **Profile Model**: Stores user profile information such as name, email, profile picture, and more.
- **Profile Form**: Allows users to edit their profile information.
- **Profile View**: Handles the logic for displaying and updating profile data.

### Example Code

#### Profile Model (`customers/models.py`):
```python
from django.db import models
from django.contrib.auth.models import User

class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    avatar = models.ImageField(upload_to='avatars/', null=True, blank=True)
    bio = models.TextField(null=True, blank=True)

    def __str__(self):
        return self.user.username
```

#### Profile Form (`customers/forms.py`):
```python
from django import forms
from .models import Profile

class ProfileForm(forms.ModelForm):
    class Meta:
        model = Profile
        fields = ['avatar', 'bio']
```

#### Profile View (`customers/views.py`):
```python
from django.shortcuts import render, redirect
from django.contrib.auth.decorators import login_required
from .forms import ProfileForm

@login_required
def profile_view(request):
    profile = request.user.profile
    if request.method == 'POST':
        form = ProfileForm(request.POST, request.FILES, instance=profile)
        if form.is_valid():
            form.save()
            return redirect('profile')
    else:
        form = ProfileForm(instance=profile)
    return render(request, 'customers/profile.html', {'form': form})
```

<br />

---

## License

This project is open-source and available under the [MIT License](LICENSE). Feel free to use, modify, and distribute it as needed.

<br />

---

## Contact

If you have any questions or suggestions, feel free to reach out:

- **GitHub**: [salahsaeed19](https://github.com/salahsaeed19)
- **Email**: [salahsaef40@gmail.com](mailto:salahsaef40@gmail.com)
- **Website**: [RCM Engineering](https://rcm-eng.com/)
