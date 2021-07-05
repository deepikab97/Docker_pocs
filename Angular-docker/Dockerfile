#Stage 1-build

FROM node:12.7-alpine AS build

#define our current path inside of the container
WORKDIR /usr/src/app

#copying two files to our work directory 
COPY package.json package-lock.json ./

#force cleaning the cache of node otherwise it can throw an error of core-js being outdated and installing the node packages from the package.json
RUN npm cache clean --force
RUN npm i

#again copying the files into the image
COPY . .

#build our angular application
RUN npm run build



### STAGE 2: Run ###
FROM nginx:1.17.1-alpine
#copy the dist-output from our first image (called build, remember?) to our new image. Precisely into the NGINX public folder.
COPY --from=build /usr/src/app/dist/Angular-docker /usr/share/nginx/html