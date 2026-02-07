# ---------- Base ----------
FROM python:3.11-slim

# Prevent log buffering + .pyc files
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

# ---------- Create user ----------
RUN useradd -m -s /bin/bash job-consumer    

# ---------- Workdir ----------
WORKDIR /app

# ---------- Install dependencies ----------
RUN pip install --no-cache-dir psycopg2-binary

# ---------- Copy code ----------
COPY consumer.py .

# Give ownership to the user
RUN chown -R job-consumer:job-consumer /app

# Switch to non-root user
USER job-consumer

# ---------- Run ----------
CMD ["python3", "-u", "consumer.py"]

