# Use a base image that supports systemd, for example, Ubuntu
FROM ubuntu:20.04

# Install necessary packages
RUN apt-get update && \
    apt-get install -y shellinabox wget openssh-server sudo && \
    apt-get install -y systemd && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN useradd -m -p $(openssl passwd -1 Rabiu2004@) -s /bin/bash rhsalisu
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

# Download and run aapanel installation script without prompts
RUN wget -O install.sh http://www.aapanel.com/script/install-ubuntu_6.0_en.sh && \
    chmod +x install.sh && \
    bash install.sh aapanel && \
    rm install.sh

RUN echo 'root:root' | chpasswd

# Expose the web-based terminal port
EXPOSE 4200 22

# Start shellinabox
CMD ["/bin/bash", "-c", "/usr/bin/shellinaboxd -t -s '/:LOGIN' && /usr/sbin/sshd -D"]
