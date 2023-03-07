# Docker Guide
This is a guide to using docker


## Dcoker commands
```
docker run <image>
```
Will run a docker image. Flags include:
- `d` - detached, this means we can run the command without holding our browser
- `p` - port map, here we map our port

In the example below we run a docker image of an Nginx server on our localhost:
```
docker run -d -p 80:80 nginx
```
When we run this and go to our browser we should have our server up and running as shown below
### image of working nginx server

We can check images that are currently running with
```
docker ps
```
And if we want to delete any images
```
docker rm <Container ID> -f
```
The flag `f` means force

To communicate with a container we run the following
```
docker exec -it <Container ID> sh
```
`sh` implies we are communicating via shell

Note a potential blocker may arise, in which case run
```
alias docker="winpty docker"
```
We will know the command has run successfully when we get the `#` prompt which implies we are communicating with the specified container.

If we wish to edit the image, the Nginx server, we navigate to the `index.html` file located in the following directory
```
/usr/share/nginx/html
```
We can start and stop running docker container images via
```
docker start <Container ID>
```
and
```
docker stop <Container ID>
```

### Pushing a container image to Docker Hub
After making a change in a docker container image we need to commit the change before we push to docker hub. We do this by 
```
docker commit <Container ID> <repo name>
```
Then tag the image
```
docker tag <repo name>
```
Then we push
```
docker push <repo name>
```
NOTE: Regarding `<repo name>` this may appear in the format `user/image-name`, here `user` refers to the Docker Hub user name.

### Docker Build
Docker build allows us to build an image from a Dockerfile the command is as shown below:
```
docker build -t <reponame>/<image-name>:<tag> <location>
```
Note that in `<location>` you specify the location of the Dockerfile, if you are executing the command from the same directory as your Dockerfile then the location is denoted as `.`

e.g.
```
docker build -t iwparry/tech201-nginx:v1 .
```
Where the flag `-t` denotes tag (v1 in this case), and we are building this image in the repository `iwparry/tech201-nginx` with tag `v1` on DockerHub, and this command was ran in the same directory as our Dockerfile.

### Downloading dockers documentation to our localhost
Docker has provided us with a way to download their entire documentation to our localhost, accessible even if we aren't connected to the internet.

The command we run to do this is
```
docker run -d -p 4000:4000 docs/docker.github.io
```
Now Docker's documentation is available to view on our localhost via port 4000.

