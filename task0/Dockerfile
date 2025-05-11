FROM ubuntu:latest

# Set working directory
WORKDIR /app

# Update package list and upgrade installed packages
RUN apt-get update && \
    apt-get upgrade -y && \
    rm -rf /var/lib/apt/lists/*

# Copy any application files (if needed)
# COPY . .

# Set default command to echo Hello, World!
CMD ["echo", "Hello, World!"] 