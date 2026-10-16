FROM python:3.13-slim AS build

WORKDIR /app

COPY requirements.txt ./
RUN pip install --no-cache-dir --target=/deps -r requirements.txt

COPY . .

FROM gcr.io/distroless/python3-debian13:nonroot AS final

WORKDIR /app

COPY --from=build /deps /deps
COPY --from=build /app /app

ENV PYTHONPATH="/deps:/app"

EXPOSE 80

CMD ["app.py"]
