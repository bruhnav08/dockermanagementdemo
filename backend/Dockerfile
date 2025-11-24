# Use Python 3.10 slim image for a small footprint
FROM python:3.10-slim

# Set working directory
WORKDIR /app

# Install system dependencies (if needed for specific python packages)
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first to leverage Docker cache
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY . .

# Expose the port Flask runs on (internal to Docker network)
EXPOSE 5000

# Command to run the app using Gunicorn (Production Server)
# -w 4: 4 worker processes
# -b 0.0.0.0:5000: Bind to all interfaces on port 5000
CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:5000", "app:app"]