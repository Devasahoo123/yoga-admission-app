# Step 1: Use the official Node.js image
FROM node:16-alpine

# Step 2: Set the working directory inside the container
WORKDIR /app

# Step 3: Copy package.json and package-lock.json files
COPY package*.json ./

# Step 4: Install dependencies
RUN npm install

# Step 5: Copy the rest of the backend code to the container
COPY . .

# Step 6: Expose the port the backend will run on
EXPOSE 5000

# Step 7: Start the Express server
CMD ["node", "server.js"]
