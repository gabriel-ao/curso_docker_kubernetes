FROM python:3

# RUN apt-get update -y && \
#     apt-get install -y python3-pip python-dev

RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

RUN pip install Flask
RUN pip install requests


COPY . . 

EXPOSE 5000

CMD ["python", "./app.py"]



