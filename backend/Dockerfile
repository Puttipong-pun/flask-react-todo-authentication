# Use official python slim image
FROM python:3.13-slim

# Install system dependencies required for mysqlclient
RUN apt-get update && apt-get install -y \
    pkg-config \
    default-libmysqlclient-dev \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Install pip dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy source code
COPY . .

# Run gunicorn server
CMD exec gunicorn --bind :$PORT --workers 1 --threads 8 --timeout 0 main:app
