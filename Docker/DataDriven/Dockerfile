# Use the official Node.js 20 image as the base image
FROM node:22

# Set the working directory in the container
WORKDIR /app

#Install Newman Reporter HTMLExtra
RUN npm install -g newman newman-reporter-html newman-reporter-htmlextra


# Copy your Postman collection and environment files to the working directory, .(dot) means go to current working directory
COPY DataDriven.json .
COPY NewTextDocument1.csv .

# Set the command to run Newman and execute your Postman collection
CMD ["newman", "run", "DataDriven.json", "-d", "NewTextDocument1.csv", "-r", "cli,json,html,htmlextra"]