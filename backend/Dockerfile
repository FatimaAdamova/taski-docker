FROM python:3.12-alpine

RUN apk update && apk add --no-cache \
    gcc \
    musl-dev \
    python3-dev \
    libffi-dev \
    postgresql-dev

RUN pip install --upgrade pip setuptools && \
    python -c "import setuptools; import sys; sys.path.insert(0, setuptools.__path__[0] + '/.distutils'); import distutils"
RUN pip install gunicorn==23.0.0
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt --no-cache-dir --progress-bar off
COPY . .
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "backend.wsgi"]