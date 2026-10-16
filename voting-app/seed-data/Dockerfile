FROM python:3.11-slim
WORKDIR /app

# hadolint ignore=DL3008
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends apache2-utils \
    && rm -rf /var/lib/apt/lists/*

RUN pip uninstall -y wheel jaraco.context || true
COPY . .
RUN python make-data.py && chmod +x generate-votes.sh
CMD ["/app/generate-votes.sh"]
