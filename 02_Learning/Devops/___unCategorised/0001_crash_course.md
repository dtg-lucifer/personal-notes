---
tags:
  - devops
  - learning
---
# What we will learn today? 
We will learn how to build and deploy a simple nodejs application made with express. Which will have the featuer of rolling updates and the stage wise building with docker and finally deploying that on to a AWS instance. 

**The basic diagram of our todays learning**
![[Pasted image 20240724225552.png]]

So bascially we will containerise a Nodejs app made with express and deploy that with rolling updates and some more basic concepts about DevOps on to as AWS EC2 instance

Read more about docker - [[0002_docker#What is Docker]]

# Setup
Setting up this project us too easy just create an express app with type script and just make the `Dockerfile` which is the main entry point of our container. 
Which looks like 

```dockerfile
FROM node:18 as builder

WORKDIR /build

COPY package*.json .
RUN npm install

COPY src/ src/
COPY tsconfig.json tsconfig.json

RUN npm run build

FROM node:18 as runner

WORKDIR /app

COPY --from=builder build/package*.json .
COPY --from=builder build/node_modules node_modules
COPY --from=builder build/dist dist/

CMD [ "npm", "start" ]
```

On the other hand the npm scripts look like this 

```json
{
	...
	"scripts": {
	    "start": "node dist/index",
	    "build": "tsc -p ."
	},
	...
}
```

After all of the above steps we also have to build the docker image with this command

```bash
docker build -t tag-for-image .
```

After that to run that also we need to run this command 

```bash
docker run -it -p your-system-port:app-port tag-for-image 
```

Therefore we have to push this image to an online image registry such as **AWS ECR (Elastic Container Registry)**

Therefore we have to go to the AWS sections again to deploy and add Load Balancers to this container. [Ful walkthrough](https://youtu.be/YOqUAfNtXFE?si=0-gfPR8_E2XKF09J)