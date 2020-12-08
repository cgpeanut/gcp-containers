# GCP Containers
- Create a container image with a Docker file.
- Basic Docker file looks like:
- FROM ubuntu: 18.04
- COPY . /app
- RUN make /app
- CMD python /app/ap.py
- save as Dockerfile
- $ docker build -t myapp .
- $ docker run -d myapp 

- $ docker ps
- $ docker stop container-name 
- $ docker logs conainer-name 

- $ docker images
- $ docker tag myapp gcr.io/myapp
- $ docker push gcr.io/myapp
- $ docker rmi - rmove local images

# lab: first container:
    - Use Google Cloud Shell
    - Create a Python app in Docker
    - Run and interact with local containers
    - Tag a Docker image and push to a regitry
    - All this in Gioogle Cloud Console (projet)
      - enable container registry API (Apis and Services)
      - click on cloud shell 
            - $ mkdir myapp
            - $ cd myapp
            - $ vim server.py
```
```
```
### start of server.py ###

import tornado.ioloop
import tornado.web

class MainHandler(tornado.web.RequestHandler):
    def get(self):
        self.write("Hello, world\n")
        print(self.request)


def make_app():
    return tornado.web.Application([
        (r"/", MainHandler),
    ])


if __name__ == "__main__":
    app = make_app()
    app.listen(8888)
    tornado.ioloop.IOLoop.current().start()

### end of server.py ###
```
```
```
            - create requirements.txt 
              - tornado
            - creeate Dockerfile 
            - $ docker build -t myapp .
            - $ docker history myapp
            - $ docker images
            - $ docker run -d -p 8888:8888 myapp
            - $ curl http://localhost:8888
            - $ docker ps 
            - $ docker logs naughty_brown
            - $ docker exec -it naughty_brown /bin/bash

```
```
```
### start of Dockerfile ###
FROM python:3.5

COPY . /app
WORKDIR /app

RUN pip install -r requirements.txt

CMD ["python", "-u", "server.py"]
```
```
```