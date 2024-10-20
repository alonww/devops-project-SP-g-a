FROM python:3.12-slim

RUN mkdir -p /opt/status-page
# Set the working directory in the container
WORKDIR /opt/status-page

# Copy the entire project into the container
COPY . .

# Install system dependencies required for PostgreSQL and other libraries
RUN apt-get update && \
apt install -y python3 python3-pip python3-venv python3-dev build-essential libxml2-dev libxslt1-dev libffi-dev libpq-dev libssl-dev zlib1g-dev

# Install the dependencies from requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Expose the port that the app will run on
EXPOSE 8001

# Run the application with Gunicorn
CMD ["gunicorn", "--pid", "/var/tmp/status-page.pid", "--pythonpath", "/opt/status-page/statuspage", "--config", "/opt/status-page/gunicorn.py", "statuspage.wsgi:application", "--bind", "0.0.0.0:8001"]

