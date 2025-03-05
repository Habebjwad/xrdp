# Use an Ubuntu base image
FROM ubuntu:22.04

# Prevent interactive prompts during package installs
ENV DEBIAN_FRONTEND=noninteractive

# Update and install desktop environment, RDP server, and utilities
RUN apt-get update && apt-get install -y \
    xfce4 \
    xfce4-goodies \
    xorg \
    dbus-x11 \
    xrdp \
    sudo \
    && apt-get clean

# Create a default user and configure sudo (adjust username as needed)
RUN useradd -ms /bin/bash codespace && echo "codespace:codespace" | chpasswd && adduser codespace sudo

# Set the default user (Codespaces usually use 'codespace')
USER codespace
WORKDIR /home/codespace

# Set up XFCE to start via RDP by writing the session file
RUN echo "xfce4-session" > ~/.xsession

# Expose the default RDP port
EXPOSE 3389

# Switch back to root for service management
USER root

# Configure xrdp to start automatically
RUN systemctl enable xrdp

# Use a simple startup command that starts xrdp in the foreground
CMD ["/usr/sbin/xrdp", "--nodaemon"]
