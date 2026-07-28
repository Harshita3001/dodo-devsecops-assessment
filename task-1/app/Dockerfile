FROM python:3.12-slim

# Create non-root user
RUN useradd -u 10001 -r -s /sbin/nologin appuser

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .

# Prepare permissions for non-root execution
RUN mkdir -p /tmp && chown -R appuser:appuser /app /tmp

USER 10001

EXPOSE 8080

CMD ["python", "app.py"]
