# Use a lighter version of Node as a parent image
FROM mhart/alpine-node:12.9.1

# Set the working directory to /client
WORKDIR /client

# Address the error of RUN /wait-for-it.sh api_1 | env: can't execute 'bash': No such file or directory.  See https://stackoverflow.com/questions/40944479/how-to-use-bash-with-an-alpine-based-docker-image/40944512 
RUN apk add --no-cache bash

# https://github.com/vishnubob/wait-for-it/issues/57
COPY wait-for-it.sh /wait-for-it.sh
RUN chmod +x /wait-for-it.sh

# copy package.json into the container at /client
COPY package*.json /client/

# install dependencies
RUN npm install

# Copy the current directory contents into the container at /client
COPY . /client/

# Make port 3000 available to the world outside this container
EXPOSE 3000

# Run the app when the container launches
CMD react-scripts start