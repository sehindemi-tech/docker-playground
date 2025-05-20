FROM python:3.9-slim AS build

WORKDIR /app

RUN apt-get update && apt-get install -y \
    build-essential \
    default-libmysqlclient-dev \
    gcc \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

COPY . .

RUN pip install --upgrade pip && \
    pip install --prefix=/install flask mysqlclient


FROM python:3.9-slim 

WORKDIR /app

RUN apt-get update && apt-get install -y \
    default-libmysqlclient-dev \
    && rm -rf /var/lib/apt/lists/*

COPY --from=build /install /usr/local/

COPY --from=build /app /app

EXPOSE 5002

CMD ["python", "app.py"]