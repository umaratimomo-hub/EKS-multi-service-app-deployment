FROM python:3.11-slim
WORKDIR /app

# hadolint ignore=DL3008
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends apache2-utils \
    && apt-get purge -y python3-wheel python3-jaraco.context || true \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*
RUN pip install --no-cache-dir setuptools==78.1.1 wheel==0.46.2 jaraco.context==6.1.0
COPY . .
RUN python make-data.py && chmod +x generate-votes.sh
CMD ["/app/generate-votes.sh"]
