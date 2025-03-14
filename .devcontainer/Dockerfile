FROM debian:bookworm

# Install all required packages including git, build tools, Java, Ruby, Node, and more.
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    git \
    build-essential \
    gdb \
    python3-pip \
    openjdk-11-jdk \
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

# Upgrade pip and install Python packages
RUN pip3 install --upgrade pip && pip3 install pwntools ROPgadget Pycryptodome

# Install Ruby gems
RUN gem install one_gadget rake zsteg

# Download Stegsolve and place it in /opt
RUN wget -O /opt/Stegsolve.jar http://www.caesum.com/handbook/Stegsolve.jar

# Clone RsaCtfTool, install its requirements, and create a symlink for easy access
RUN git clone https://github.com/RsaCtfTool/RsaCtfTool.git /opt/RsaCtfTool && \
    cd /opt/RsaCtfTool && \
    pip3 install -r requirements.txt && \
    ln -s /opt/RsaCtfTool/RsaCtfTool.py /usr/local/bin/rsactftool

# Download Recaf and place it in /opt
RUN wget -O /opt/recaf.jar https://github.com/Col-E/Recaf/releases/download/2.21.13/recaf-2.21.13-J8-jar-with-dependencies.jar

# Create the "vscode" user as it is expected later in the Dockerfile.
RUN useradd -ms /bin/bash vscode

USER vscode

SHELL ["/bin/bash", "-c"]

# Install GEF for GDB enhancements
RUN bash -c "$(curl -fsSL https://gef.blah.cat/sh)"

# Ensure the default shell for vscode is set to bash
RUN usermod -s /bin/bash vscode

# Configure aliases and environment variables for the vscode user
RUN echo "export LC_CTYPE=C.UTF-8; alias python=python3; alias stegsolve='java -jar /opt/Stegsolve.jar'; alias recaf='java -jar /opt/recaf.jar'" >> /home/vscode/.shinit
RUN echo "ENV=\$HOME/.shinit; export ENV" >> /home/vscode/.profile
