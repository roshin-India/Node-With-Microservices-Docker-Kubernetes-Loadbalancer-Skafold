# Specify base image
FROM node:14-alpine

WORKDIR /usr/app
# If we get any error related file like package.json not found
# COPY ./package.json ./ 
COPY ./package.json ./ 
# Step 2: Download and install dependency
RUN npm install

# If wany changes made in project file. We dont need to re run entile npm install step
# We can avoid those changes by making this step 
# COPY ./ ./ 
COPY ./ ./
# Step 3: Tell the image what to do when it starts as container

CMD ["npm" , "start"]