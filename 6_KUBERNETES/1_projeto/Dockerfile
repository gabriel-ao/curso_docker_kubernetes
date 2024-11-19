FROM python:3

RUN apt-get update -y && \
  apt-get install -y python3-pip python3-dev

WORKDIR /app

RUN pip install Flask

COPY . .

EXPOSE 5000

CMD [ "python", "./app.py" ]

# docker run -d -p 5000:5000 --name flash-hub --rm gabrieloliveira/flask-hub-projeto