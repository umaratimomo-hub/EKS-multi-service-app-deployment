FROM python:3.13-slim AS build

WORKDIR /app

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

FROM gcr.io/distroless/python3-debian13:nonroot AS final

WORKDIR /app

COPY --from=build --chown=nonroot:nonroot /app/ /app/
#COPY --from=build /install /install

#ENV PYTHONPATH=/install

EXPOSE 80

CMD ["python", "app.py"]

#curl=7.88.1-10+deb12u15
