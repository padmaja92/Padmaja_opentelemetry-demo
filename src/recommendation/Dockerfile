FROM python:3.11-slim AS builder

WORKDIR /usr/src/app

COPY requirements.txt ./
COPY . .

RUN python -m pip install --upgrade pip
RUN pip install -r requirements.txt
ENTRYPOINT [ "python", "recommendation_server.py" ]

