# Getting Started with Docker React App

Reference Link: https://www.pluralsight.com/guides/using-react.js-with-docker

#### Install Docker

Download for Windows:
```
https://docs.docker.com/desktop/windows/install/
```

Check docker installed:
> docker --version

Run the installer and follow the below steps:
1. Go to "Windows Features"
2. Enable "Virtual Machine Platform"
3. Enable "Windows subsystem for Linux"
4. Enable "Hyper-V"
5. Restart your machine
6. Go to BIOS setting
7. Find "Virtualization" option from "System Configuration > Virtualization Technology"
8. Enable Virtualization
9. Restart your machine
10. Go to this "https://docs.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package" to download the linux kernel update
11. Install the update
12. Run command in CMD
> wsl --set-default-version 2

#### Create React App

Run following command to create react app
```
npx create-react-app docker-react-app
```

Create a Dockerfile:
```
# pull the base image
FROM node:alpine

# set the working direction
WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install app depdendencies
COPY package.json ./

COPY package-lock.json ./

RUN npm install

# add app
COPY . ./

# start app
CMD ["npm", "start"]
```

Create a .dockerignore file:
```
node_modules
npm-debug.log
build
.dockerignore
**/.git
**/.DS_Store
**/node_modules
```

#### Build Docker Container

Run following command to build image:
```
docker build -t ps-container:dev .
```
Check your container:
```
docker image ls
```

#### Run Docker Container

Run following command to build image:
```
docker run -it --rm -v "%cd%":/app -v /app/node_modues/ -p 3001:3000 -e CHOKIDAR_USEPOLLING=true ps-container:dev
```
For windows "%cd%" instead of ${PWD}

Check your application on: http://localhost:3001/
