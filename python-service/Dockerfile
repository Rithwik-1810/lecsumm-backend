FROM python:3.10

# Install ffmpeg and git (git needed to clone whisper)
RUN apt-get update && apt-get install -y ffmpeg git && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Upgrade pip and setuptools
RUN pip install --no-cache-dir --upgrade pip setuptools wheel

# Install dependencies from requirements.txt (everything except whisper)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Clone and install whisper without its dependencies (already installed)
RUN git clone https://github.com/openai/whisper.git /tmp/whisper && \
    cd /tmp/whisper && \
    pip install --no-cache-dir --no-deps . && \
    rm -rf /tmp/whisper

COPY . .

CMD ["gunicorn", "app:app", "--bind", "0.0.0.0:5001"]