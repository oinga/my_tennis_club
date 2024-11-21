# Use an official Python runtime as a parent image
FROM python:3.10-slim

# Set environment variables
# Prevent Python from writing .pyc files
ENV PYTHONDONTWRITEBYTECODE=1
# Ensure Python output is shown in logs   
ENV PYTHONUNBUFFERED=1    

# Set the working directory inside the container
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libpq-dev gcc \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Python dependencies individually
RUN pip install --no-cache-dir asgiref==3.8.1
RUN pip install --no-cache-dir Django==5.1.1
RUN pip install --no-cache-dir psycopg2-binary==2.9.9
RUN pip install --no-cache-dir sqlparse==0.5.1
RUN pip install --no-cache-dir tzdata==2024.2
RUN pip install --no-cache-dir whitenoise==6.7.0

# Copy the entire project into the container
COPY . /app/

# Collect static files
RUN python manage.py collectstatic --noinput

# Expose the port Django runs on
EXPOSE 8000

# Use Gunicorn to serve the application in production
CMD ["gunicorn", "myproject.wsgi:application", "--bind", "0.0.0.0:8000"]
