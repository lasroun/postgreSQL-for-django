# PostgreSQL for Django Setup Guide

This guide explains how to set up PostgreSQL for your Django project in one single file.

## Step 1: Install psycopg2

Install the `psycopg2` package in your Django environment by running:

```bash
pip install psycopg2
```

## Step 2: Configure PostgreSQL

### Create a User and a Database

Connect to PostgreSQL using `psql` and run the following commands:

```sql
-- Create a new user with an encrypted password
CREATE USER user WITH ENCRYPTED PASSWORD 'password';

-- Set client encoding and transaction isolation for the user
ALTER ROLE user SET client_encoding TO 'utf8';
ALTER ROLE user SET default_transaction_isolation TO 'read committed';

-- Create a new database and grant all privileges to the user
CREATE DATABASE database;
GRANT ALL PRIVILEGES ON DATABASE database TO user;
```

## Step 3: Update Django Settings

In your Django project's `settings.py` file, update the `DATABASES` setting as follows:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'database',
        'USER': 'user',
        'PASSWORD': 'password',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```

## Step 4: Useful psql Commands

- **Connect to the database:**

  ```bash
  \c database
  ```

- **List all tables in the connected database:**

  ```bash
  \dt
  ```

**Note:** Replace `user`, `password`, and `database` with your actual credentials.
