# ---------- Base ----------
FROM python:3.11-slim

# Prevent log buffering + .pyc files
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

# ---------- Create user ----------
RUN useradd -m -s /bin/bash job-pusher    

# ---------- Workdir ----------
WORKDIR /app

# ---------- Install dependencies ----------
RUN pip install --no-cache-dir psycopg2-binary

# ---------- Copy code ----------
COPY pusher.py .

# Give ownership to the user
RUN chown -R job-pusher:job-pusher /app

# Switch to non-root user
USER job-pusher

# ---------- Run ----------
CMD ["python3", "-u", "pusher.py"]

