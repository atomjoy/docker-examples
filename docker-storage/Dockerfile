# Stage build target frontend1
FROM nginx:bookworm AS frontend1

# Update & install
RUN apt-get update -y
RUN apt-get install nano -y

# Create dir
WORKDIR /home/test/app

# Stage build target frontend2
FROM nginx:bookworm AS frontend2

# Update & install
RUN apt-get update -y
RUN apt-get install nano -y

# Create dir
WORKDIR /home/test/app