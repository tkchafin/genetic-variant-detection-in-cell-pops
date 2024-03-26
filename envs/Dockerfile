# Use Ubuntu as the base image
FROM --platform=linux/amd64 ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

# Update and install dependencies
RUN apt-get update && apt-get install -y \
    wget \
    git \
    bcftools \
    tabix \
    libvcflib-tools \
    libvcflib-dev \
    python3 \
    parallel \
    && rm -rf /var/lib/apt/lists/*

# python dependencies
RUN apt-get update && apt-get install -y python3-pip \
    && python3 -m pip install pysam

# Download Freebayes static binary
RUN wget -q https://github.com/freebayes/freebayes/releases/download/v1.3.6/freebayes-1.3.6-linux-amd64-static.gz -O /tmp/freebayes.gz \
    && gunzip /tmp/freebayes.gz \
    && chmod +x /tmp/freebayes \
    && mv /tmp/freebayes /usr/local/bin/

# Clone the Freebayes repository and symlink scripts
RUN git clone --recursive https://github.com/freebayes/freebayes.git /opt/freebayes \
    && ln -s /opt/freebayes/scripts/* /usr/local/bin/

# Clone the genetic-variant-detection-in-cell-pops repository and symlink scripts
RUN git clone https://github.com/glaParaBio/genetic-variant-detection-in-cell-pops.git /opt/genetic-variant-detection \
    && ln -s /opt/genetic-variant-detection/scripts/* /usr/local/bin/

# Set the default command for the container
CMD ["bash"]
