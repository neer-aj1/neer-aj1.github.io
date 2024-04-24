---
title: "Docker IA"
date: 2019-04-18T15:34:30-04:00
categories:
  - blog
tags:
  - Jekyll
  - update
---
I have made a three tier web application using React for frontend, NodeJs for backend and mongoDB for server. For mongoDB I have used the offical mongoDB image and for frontend and backend I have created the images using Dockerfile. 
<br>
Below are the steps I have followed to achieve this.
Assuming that the frontend and backend codes are already reacted.

#### STEP 1:

Create a repository in docker hub.
![Docker-hub](/assets/images/image.png)

#### STEP 2:
Make dockerfile for the frontend like below:
![Dockerfile-frontend](/assets/images/Screenshot%202024-04-24%20113511.png)
1. FROM node:latest: Base the image on the latest Node.js image.
2. WORKDIR /app: Set the working directory inside the container to /app.
3. COPY package*.json ./: Copy package.json and package-lock.json (if present) to the container.
4. RUN npm install: Install dependencies specified in package.json.
5. COPY . .: Copy the application code to the container.
6. EXPOSE 5173: Inform Docker that the container will listen on port 5173 (but does not actually publish it).
7. CMD ["npm", "run", "dev"]: Set the default command to run the application in development mode using npm.

#### STEP 3:
Make dockerfile for the backend like below:
![Dockerfile-backend](/assets/images/Screenshot%202024-04-24%20113930.png)
1. FROM node:latest: Base the image on the latest Node.js image.
2. COPY package*.json ./: Copy package.json and package-lock.json (if present) to the container.
3. RUN npm install: Install dependencies specified in package.json.
4. COPY . .: Copy the application code to the container.
5. EXPOSE 5000: Inform Docker that the container will listen on port 5000 (but does not actually publish it).
6. CMD ["node", "index.js"]: Set the default command to run the Node.js application, specifically starting the index.js file.

#### STEP 4:
Pull mongo image:
![Dockerfile-mongo](/assets/images/Screenshot%202024-04-24%20114308.png)

#### STEP 5:
Run mongo image:
![Dockerfile-mongo](/assets/images/Screenshot%202024-04-24%20104654.png)

#### STEP 6:
Build frontend and backend images:
![Dockerfile-mongo](/assets/images/Screenshot%202024-04-24%20114601.png)
<br>

![Dockerfile-mongo](/assets/images/Screenshot%202024-04-24%20114653.png)

#### STEP 7:
Run backend and frontend images in containers:
![Dockerfile-mongo](/assets/images/Screenshot%202024-04-24%20114856.png)
<br>

![Dockerfile-mongo](/assets/images/Screenshot%202024-04-24%20114903.png)


#### STEP 8:
Push frontend and backend images to docker hub:
![Dockerfile-mongo](/assets/images/Screenshot%202024-04-24%20115040.png)
<br>

![Dockerfile-mongo](/assets/images/Screenshot%202024-04-24%20115056.png)

#### OUTPUTS
After running the containers we'll get the below outputs:
![Dockerfile-mongo](/assets/images/Screenshot%202024-04-24%20105507.png)
<br>

![Dockerfile-mongo](/assets/images/Screenshot%202024-04-24%20115251.png)
<br>

![Dockerfile-mongo](/assets/images/Screenshot%202024-04-24%20105645.png)
