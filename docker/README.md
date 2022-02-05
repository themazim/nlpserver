# NLP Server Docker image

Docker slim image with NLP Server
 
## Image creation

Inside the docker folder run 
```
 # execute from root folder
 docker build . --tag nlpserver:1.0 --progress plain -f docker/Dockerfile

 docker run --publish 6400:6400 --detach --name nlpserver nlpserver:1.0  

```

For CoreNLP on another container run:
```
docker run -p 9000:9000 nlpbox/corenlp
``` 