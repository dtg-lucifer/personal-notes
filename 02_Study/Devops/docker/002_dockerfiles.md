
# What is a docker file

A docker file a manifest which tells docker to build a image specific to our needs depending on the dockerfile. Basically when you run docker it will look for a file named **Dockerfile** at the root.

# Example dockerfile

```dockerfile
FROM node:alpine AS build
LABEL maintainer="Piush Bose <dev.bosepiush@gmail.com>"

WORKDIR /app

COPY package*.json ./
RUN npm install
  
COPY . .

RUN npm run build
  
FROM node:alpine AS publish
LABEL maintainer="Piush Bose <dev.bosepiush@gmail.com>"
LABEL github="https://github.com/snappy-hq/snappy-notes"
  
WORKDIR /src  

COPY --from=build /app/.next ./.next
COPY --from=build /app/package*.json ./
COPY --from=build /app/public ./public
COPY --from=build /app/next.config.mjs ./next.config.mjs
  
RUN npm install --omit=dev

EXPOSE 3000

LABEL vendor="Snappy notes"
LABEL description="The official web app pf Snappy notes, built with the power of Next.js"
LABEL version="1.0"
LABEL license="MIT"
  
USER nobody

CMD ["npm", "start"]
```

This is the main docker file to build our project #snappy-notes , more specifically the frontend of that with this file using nextjs
