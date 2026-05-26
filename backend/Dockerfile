# Django 6.0 requires Python 3.12+

FROM python:3.12-slim

WORKDIR /app

# Install system dependencies (needed for some python packages)

RUN apt-get update && apt-get install -y --no-install-recommends \
	build-essential \
	libpq-dev \
	&& rm -rf /var/lib/apt/lists/*


# Create virtualenv
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Install Python dependencies
COPY requirements.txt /app/

RUN pip install --upgrade pip && pip install -r requirements.txt

COPY . /app/

# EXPOSE port 8000

EXPOSE 8000

# Use Gunicorn for production; replace 'myproject' with your actual project na,e

CMD ["gunicorn", "--bind", "0.0.0.0:8000", "config.wsgi:application"]
