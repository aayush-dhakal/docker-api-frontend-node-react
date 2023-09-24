FROM node:17-alpine

RUN npm install -g nodemon

# working inside app directoy in docker image
WORKDIR /app

COPY package.json .

RUN npm install

# copies from current working directory(ie inside api directory) to app directory
COPY . .

# required for docker desktop port mapping. no need for it if we are running container from command line
EXPOSE 4000

#  this CMD command will run once the container is runned. 
# don't use:
# RUN node app.js coz this will excute the command on image build itself which we don't want
# CMD ["node", "app.js"]
CMD ["npm", "run", "dev"]

# command for building the image:
# => docker build -t myapp . 
# here -t is for tag which is used to define image name as myapp
# if you wish to create an image with version then define tag name for them using : after image name
# => docker build -t myapp:v1 . 

# run the container from the image:
# => docker run --name myapp_c1 -p 4000:4000 -d myapp
# if image has version name then
# => docker run --name myapp_c1 -p 4000:4000 -d myapp:v1
# here myapp_c1 is container name for image myapp and -p is used to map the port on docker where right 4000 is the port exposed by the container and the port on left is the port that we want to map. (So you can basically also write -p 5000:4000 which mapes our apps 5000 port to docker 4000 port.) The -d flag is used for datached mode which basically doesn't block our terminal when the docker container is running

# included nodemon
# run the container and delete it immediately once it is stopped. dont use -d detached mode as we need nodemon to listen for changes constantly
# => docker run --name myapp_c1 -p 4000:4000 --rm myapp:v1

# to stop the container 
# first view the running containers by hitting: => docker ps
# then to stop the container:
# => docker stop container_id or docker stop docker_name
# example: docker stop myapp_c1 or docker stop be967d8adb4a

# to see the all the container even though the ones that are not running hit: => docker ps -a
# to run an existing terminated container(note while restarting the container we do not need to map the port again) hit: => docker start myapp_c2 

# to delete an image:
# => docker image rm image_name
# note to delete image, it should not be used any containers(even if the container are not running but have used the image then you won't be able to delete it)
# to delete the image even if the container is using it use force flag:
# => docker image rm image_name -f

# to delete a container
# => docker container rm container_name another_container_name_if_any

# to delete all containers all images and all volumes(the containers must not be in running state or else it wont remove)
# docker system prune -a

# mapping the volume so that the changes are reflected even if the image is not re built
# docker run --name myapp_c1 -p 4000:4000 --rm -v D:\programming learning\2023\docker\1 net ninja\api\:/app -v /app/node_modules myapp:v1