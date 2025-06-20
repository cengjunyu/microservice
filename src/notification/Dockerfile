FROM python:3.10-slim-bullseye

ENV PYTHONUNBUFFERED=1

RUN sed -i 's/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list  # ❗ 修正：security.debian.org 也需要替换

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential ffmpeg && \
    rm -rf /var/lib/apt/lists/*

RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

WORKDIR /app
COPY ./requirements.txt /app/
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir --requirement /app/requirements.txt

COPY . /app/

CMD ["python3", "consumer.py"]