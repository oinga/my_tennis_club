# Use an official Python runtime as a parent image
FROM python:3.10-slim

# Set environment variables

# Prevent Python from writing .pyc files
ENV PYTHONDONTWRITEBYTECODE=1  
# Ensure Python output is shown in logs  
ENV PYTHONUNBUFFERED=1           

# Set the working directory
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libpq-dev gcc \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Copy requirements.txt and install Python dependencies
COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt

# Copy the entire project into the container
COPY . /app/

# Collect static files
RUN python manage.py collectstatic --noinput

# Expose the port Django runs on
EXPOSE 8000

# Use Gunicorn to serve the application in production
CMD ["gunicorn", "myproject.wsgi:application", "--bind", "0.0.0.0:8000"]
