# Use latest Debian (Bookworm)
FROM debian:bookworm

# Set non-interactive frontend to avoid prompts
ENV DEBIAN_FRONTEND=noninteractive

# Update package lists and install necessary packages
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
    git \
    build-essential \
    gdb \
    python3-pip \
    openjdk-17-jdk \
    ruby-dev \
    npm \
    wget \
    unzip \
    file \
    netcat \
    wireshark \
    audacity \
    firefox-esr \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Set default working directory
WORKDIR /workspace

# Verify installation
RUN git --version && g++ --version && python3 --version && java --version && ruby --version && node --version

# Set entry point
CMD ["/bin/bash"]
