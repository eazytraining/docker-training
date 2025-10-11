FROM python:3.14-slim

LABEL maintainer="Eazytraining <contact@eazytraining.fr>" \
      description="Pozos API Student List"

# Set working directory
WORKDIR /app

# Copy requirements first for better layer caching
COPY requirements.txt .

# Install system dependencies
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
        python3-dev \
        libsasl2-dev \
        libldap2-dev \
        libssl-dev \
        gcc \
        build-essential && \
    rm -rf /var/lib/apt/lists/*

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY student_age.py .

# Create volume mount point
VOLUME /data

# Expose application port
EXPOSE 5000

# Run the application
CMD ["python3", "./student_age.py"]