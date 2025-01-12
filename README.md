# Authentication Service for prohub.uz Online Learning Platform

This project is an **Authentication Service** for an online learning platform. It helps manage user accounts, including registration with email confirmation, logging in, updating or deleting profiles, and admin tools for managing users.  

The project is built using **Django REST Framework (DRF)** and uses **PostgreSQL** as its database. This documentation will guide you through setting up, running, and using this service.  

---

## Features  

### User Features  
1. **Register**: Users can create an account by providing their email and password. An email is sent to confirm registration.  
2. **Login**: Users can log in to their account and get a token for authentication.  
3. **Profile Management**:  
   - View your profile.  
   - Update or delete your profile as needed.  
4. **Get Profile by ID**: Allows users to retrieve their profile using their unique user ID.  

### Admin Features  
- Manage all users through Django’s custom admin tools and commands.  

---

## Technologies Used  

- [![Django](https://static.djangoproject.com/img/logos/django-logo-negative.svg)](https://www.djangoproject.com/)  
- [![PostgreSQL](https://www.vectorlogo.zone/logos/postgresql/postgresql-ar21.svg)](https://www.postgresql.org/)
- [![RabbitMQ](https://upload.wikimedia.org/wikipedia/commons/3/31/RabbitMQ_logo.svg)](https://www.rabbitmq.com/)
- **Environment Variables**: Securely configure sensitive information like database credentials using a `.env` file.  

---

## How to Set Up the Project  

Follow these steps to set up the project on your local machine.  

### 1. Prerequisites  
Make sure you have the following installed:  
- **Python (version 3.12.3)**  
- **PostgreSQL (for the database)**  
- **Git (to clone the repository)**
- **RabbitMQ (message broker)**  

### 2. Clone the Repository  
First, download the project to your local machine.  
1. Open your terminal (or command prompt).  
2. Run this command:  
   ```bash  
   git clone https://github.com/dilshod1405/prohub.uz-authentication.git
   cd prohub.uz-authentication
   ```  

### 3. Create a Virtual Environment  
A virtual environment keeps your project’s dependencies isolated.  
1. Run this command:  
   ```bash  
   python3 -m venv venv  
   ```  
2. Activate the virtual environment:  
   - On Linux/Mac: `source venv/bin/activate`  
   - On Windows: `venv\Scripts\activate`  

### 4. Install Dependencies  
The project uses Python libraries listed in the `requirements.txt` file. To install them, run:  
```bash  
pip install -r requirements.txt  
```  

### 5. Configure Environment Variables  
This project uses a `.env` file to store sensitive information.  
1. Create a file named `.env` in the project folder.  
2. Add the following lines to it, replacing placeholders with your information:  
   ```env  
   SECRET_KEY=your_secret_key  
   DEBUG=True  
   DATABASE_NAME=your_database_name  
   DATABASE_USER=your_database_user  
   DATABASE_PASSWORD=your_database_password  
   DATABASE_HOST=127.0.0.1  
   DATABASE_PORT=5432  
   EMAIL_BACKEND=django.core.mail.backends.smtp.EmailBackend  
   EMAIL_HOST=your_smtp_server  
   EMAIL_PORT=your_smtp_port  
   EMAIL_USE_TLS=True  
   EMAIL_HOST_USER=your_email@example.com  
   EMAIL_HOST_PASSWORD=your_email_password
   RABBITMQ_URL=your_rabbitmq_url 
   ```

### 6. Set Up RabbitMQ  
Ensure RabbitMQ is running on your machine or server. Use the URL provided in the `.env` file to connect the service. 


### 7. Set Up the Database  
This project uses PostgreSQL.  
1. Open your PostgreSQL client or GUI tool and create a database.  
2. Use the database credentials you added to the `.env` file.  

Apply the database migrations by running:  
```bash  
python3 manage.py migrate  
```  

### 8. Start the Server  
Finally, start the development server by running:  
```bash  
python3 manage.py runserver  
```  
The application will be available at `http://127.0.0.1:8000/`.  

---

## How to Use the Project  

### User Registration  
- To create a new user, send a request to the `/profile/register/` endpoint with your email and password.  
- After registration, you’ll receive an email to confirm your account. Click the link in the email to activate your profile. Use `verify-email/<uuid:verification_code>/` for confirmation new user.  

### Logging In  
- Use the `/profile/login/` endpoint to log in with your email and password. You’ll get a token that must be included in the headers of future requests.  

### Profile Management  
- View your profile: `/profile/control/{id}/`  
- Update your profile: Send updated information to the same endpoint using a PUT request.  
- Delete your profile: Send a DELETE request to the same endpoint.

### Reset Password
- Send request url to user's email to reset password via `/profile/password-reset/`.
- Confirm requesting url to reset password with `/profile/password-reset-confirm/<uidb64>/<token>/`.

### Admin Commands  
As an admin, you can manage users using custom Django commands. Run commands like this:  
```bash  
python3 manage.py createsuperuser
```
- Get all users list, get user by id, update, put, patch user via `/manager/update-user/` api url. Default Router is used to manage clients beacuse of its requirement of shorter code and opportunity of rest framework.

---

## Deployment Instructions  

To deploy this project to a production environment:  
1. Set `DEBUG=False` in the `.env` file.  
2. Use a production-ready web server like Gunicorn or uWSGI to serve the application.  
3. Configure a reverse proxy like Nginx or Apache for handling incoming requests.  
4. Ensure RabbitMQ is running and reachable via the configured `RABBITMQ_URL`.   
5. Set allowed hosts in `CORS_ALLOWED_ORIGINS` to make connection with frontend.

---

## Contact  

If you have any questions or feedback, feel free to reach out:  
- **Email**: dilshod.normurodov1392@gmail.com 
- **GitHub**: https://github.com/dilshod1405
- **Telegram**: https://t.me/architect_developer

---
