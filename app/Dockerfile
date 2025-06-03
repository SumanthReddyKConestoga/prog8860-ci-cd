# Use official Python slim image
FROM python:3.9-slim

# Set working directory inside container
WORKDIR /app

# Copy application code
COPY app/ /app/

# Install Python dependencies
COPY app/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Expose Flask’s default port
EXPOSE 5000

# Command to run the Flask app
CMD ["python", "app.py"]
