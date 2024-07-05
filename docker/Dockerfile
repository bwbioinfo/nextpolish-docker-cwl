# Use a base image
FROM ubuntu:18.04

# Set non-interactive mode
ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    git \
    cmake \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    wget \
    libncurses5-dev


# Clone NextPolish repository
RUN wget https://github.com/Nextomics/NextPolish/releases/download/v1.4.1/NextPolish.tgz
RUN tar -xvzf NextPolish.tgz

# Install python3 and pip
RUN apt-get install -y python python-pip
RUN pip install paralleltask

# Build NextPolish
WORKDIR /NextPolish
RUN make

# Add NextPolish to the PATH
ENV PATH="/NextPolish/:${PATH}"

# Change the permissions of the NextPolish executable
RUN chmod +x nextPolish

# Test the installation
RUN nextPolish --version

# Set the command
CMD ["nextPolish"]

# docker build -f docker/Dockerfile -t nextpolish-test .