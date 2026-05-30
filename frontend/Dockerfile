#======== Stage 1: Build the application ======

FROM node:20-alpine AS build-stage
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./

RUN npm install

# Copy the rest of the application code 
COPY . .

# Build the project (generates the /dist folder)
RUN npm run build


# Stage 2: Serve the application with Nginx

FROM nginx:stable-alpine

RUN rm /etc/nginx/conf.d/default.conf

#Copy the build output from the previous satge
COPY  --from=build-stage /app/dist /usr/share/nginx/html

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]





