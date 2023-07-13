FROM mcr.microsoft.com/devcontainers/base:bullseye

RUN apt update && export DEBIAN_FRONTEND=noninteractive \
    && apt install -y git build-essential gdb python3-pip ruby-dev npm wget unzip file

RUN apt install -y sagemath wireshark audacity

RUN pip3 install --upgrade pip && pip3 install pwntools ROPgadget Pycryptodome

RUN gem install one_gadget rake zsteg

RUN wget -O /opt/Stegsolve.jar http://www.caesum.com/handbook/Stegsolve.jar \
    && chmod +x /opt/Stegsolve.jar

RUN git clone https://github.com/RsaCtfTool/RsaCtfTool.git /opt/RsaCtfTool \
    && cd /opt/RsaCtfTool \
    && pip3 install -r requirements.txt \
    && ln -s /opt/RsaCtfTool/RsaCtfTool.py /usr/local/bin/rsactftool

RUN bash -c "$(curl -fsSL https://gef.blah.cat/sh)"

RUN echo "export LC_CTYPE=C.UTF-8; alias python=python3; alias stegsolve='java -jar /opt/Stegsolve.jar'" >> /root/.bashrc
