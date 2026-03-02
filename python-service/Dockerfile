FROM python:3.10

# Install system dependencies: ffmpeg, git, and build tools
RUN apt-get update && apt-get install -y \
    ffmpeg \
    git \
    build-essential \
    python3-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Upgrade pip, setuptools, and wheel
RUN pip install --no-cache-dir --upgrade pip setuptools wheel

# First install all dependencies that have binary wheels (so no compilation needed)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Now install openai-whisper WITHOUT build isolation, using the already upgraded setuptools
RUN pip install --no-cache-dir --no-build-isolation openai-whisper==20231117

COPY . .

CMD ["gunicorn", "app:app", "--bind", "0.0.0.0:5001"]