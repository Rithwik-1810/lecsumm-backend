FROM python:3.10

# Install ffmpeg (still needed)
RUN apt-get update && apt-get install -y ffmpeg && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Upgrade pip, setuptools, and wheel
RUN pip install --no-cache-dir --upgrade pip setuptools wheel

COPY requirements.txt .

# Install dependencies WITHOUT build isolation (uses system setuptools)
RUN pip install --no-cache-dir --no-build-isolation -r requirements.txt

COPY . .

CMD ["gunicorn", "app:app", "--bind", "0.0.0.0:5001"]