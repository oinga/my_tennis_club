# Use an official Python runtime as a parent image
FROM python:3.10-slim

# Set environment variables
 # Prevent Python from writing .pyc files
ENV PYTHONDONTWRITEBYTECODE=1 
# Ensure Python output is shown in the logs
ENV PYTHONUNBUFFERED=1        

# Set the working directory in the container
WORKDIR /app

# Copy requirements.txt to the working directory
COPY requirements.txt /app/

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the entire project into the container
COPY . /app/

# Expose the port Django runs on
EXPOSE 8000

# Command to run the application
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
