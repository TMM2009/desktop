FROM debian:bullseye

RUN apt update && export DEBIAN_FRONTEND=noninteractive \
    && apt install -y git build-essential gdb python3-pip openjdk-11-jdk ruby-dev npm wget unzip file netcat curl

# Install glibc 2.34 manually
RUN wget http://ftp.gnu.org/gnu/libc/glibc-2.34.tar.gz && \
    tar -xvzf glibc-2.34.tar.gz && cd glibc-2.34 && \
    mkdir build && cd build && \
    ../configure --prefix=/usr && make -j$(nproc) && make install && \
    cd / && rm -rf glibc-2.34 glibc-2.34.tar.gz

RUN apt install -y wireshark audacity firefox-esr

RUN pip3 install --upgrade pip && pip3 install pwntools ROPgadget Pycryptodome

RUN gem install one_gadget rake zsteg

RUN wget -O /opt/Stegsolve.jar http://www.caesum.com/handbook/Stegsolve.jar

RUN git clone https://github.com/RsaCtfTool/RsaCtfTool.git /opt/RsaCtfTool \
    && cd /opt/RsaCtfTool \
    && pip3 install -r requirements.txt \
    && ln -s /opt/RsaCtfTool/RsaCtfTool.py /usr/local/bin/rsactftool

RUN wget -O /opt/recaf.jar https://github.com/Col-E/Recaf/releases/download/2.21.13/recaf-2.21.13-J8-jar-with-dependencies.jar

USER vscode

SHELL ["/bin/bash", "-c"]

RUN bash -c "$(curl -fsSL https://gef.blah.cat/sh)"

RUN usermod -s /bin/bash vscode

RUN echo "export LC_CTYPE=C.UTF-8; alias python=python3; alias stegsolve='java -jar /opt/Stegsolve.jar'; alias recaf='java -jar /opt/recaf.jar'" >> /home/vscode/.shinit
RUN echo "ENV=$HOME/.shinit; export ENV" >> /home/vscode/.profile
