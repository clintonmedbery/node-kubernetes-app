
#### Build the image

`docker build -t clintomed/hello-kubernetes:0.1.0 .`

#### Run an image

`docker run -p 3000:3000 -d hello-kubernetes`

#### Push the image

`docker push clintomed/hello-kubernetes:0.1.0`