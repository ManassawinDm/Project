# Start with a Python base image
FROM python:3.7

# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - \
    && apt-get update && apt-get install -y nodejs

# Set the working directory in the container
WORKDIR /usr/src/app

# Upgrade pip, setuptools, and wheel
RUN python3 -m pip install --upgrade pip setuptools wheel

# Copy the Python requirements file and install Python dependencies
COPY ./python/requirements.txt .
RUN pip3 install --no-cache-dir -r requirements.txt

# Copy the Node.js package.json and package-lock.json files
COPY package*.json ./

# Install Node.js dependencies
RUN npm cache clean --force && npm install

# Copy the rest of your application code to the container
COPY . .

# Inform Docker that the container listens on the specified network port at runtime.
EXPOSE 8112

# Use a shell script to start both Node.js and Python applications
COPY start-app.sh .
RUN chmod +x start-app.sh
CMD ["./start-app.sh"]
