# Dockerfile for YouTube Viewer Bot
FROM python:3.11-slim

# Install system dependencies
RUN apt-get update && apt-get install -y \
    wget \
    gnupg \
    unzip \
    curl \
    xvfb \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Install Google Chrome (método moderno sin apt-key)
RUN wget -q https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && apt-get update \
    && apt-get install -y ./google-chrome-stable_current_amd64.deb \
    && rm google-chrome-stable_current_amd64.deb \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN mkdir -p /app/chrome_profiles && chmod 755 /app/chrome_profiles

ENV DISPLAY=:99
ENV PYTHONUNBUFFERED=1
ENV CHROME_BIN=/usr/bin/google-chrome
ENV GOOGLE_CHROME_BIN=/usr/bin/google-chrome

EXPOSE 8080

CMD ["python3", "main.py"]
