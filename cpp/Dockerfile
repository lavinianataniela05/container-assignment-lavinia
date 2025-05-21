# Use an official Ubuntu base image
FROM ubuntu:22.04

# Install build tools (g++, make, etc.)
RUN apt-get update && apt-get install -y \
    g++ \
    make \
    cmake \
    && rm -rf /var/lib/apt/lists/*

# Set the working directory
WORKDIR /app

# Copy source code into the container
COPY . .

# Compile the program (you can replace this with a cmake command if needed)
RUN g++ -o app main.cpp

# Set the entry point to run the compiled program
CMD ["./app"]
