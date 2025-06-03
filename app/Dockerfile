# <repo-root>/app/Dockerfile

# 1. Base image
FROM python:3.9-slim

# 2. Set working directory inside container
WORKDIR /app

# 3. Copy only requirements.txt (so layer caching works)
COPY requirements.txt .

# 4. Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# 5. Copy all remaining application files into /app
COPY . .

# 6. Expose your Flask app port
EXPOSE 5000

# 7. Default command to run your Flask app
CMD ["python", "app.py"]
