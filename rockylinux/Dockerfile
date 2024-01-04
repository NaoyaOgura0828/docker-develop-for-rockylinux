# Set the base image
ARG BASE_IMAGE_TAG=${BASE_IMAGE_TAG}
FROM rockylinux:${BASE_IMAGE_TAG}

# Set ARG
ARG TZ=Asia/Tokyo
ARG USER_NAME=${USER_NAME}

# Set TimeZone
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && echo ${TZ} > /etc/timezone

# Repository Update
RUN dnf update -y

# Install Packages
RUN dnf install sudo -y &&\
    dnf install git -y &&\
    dnf install unzip -y

# Add User
RUN adduser ${USER_NAME} --badname

# Setup to use sudo without password
RUN echo "${USER_NAME} ALL=NOPASSWD: ALL" >> /etc/sudoers

# Setup WORKDIR
WORKDIR /home/${USER_NAME}

# Change User
USER ${USER_NAME}

# Setup alias
COPY ./.alias /home/${USER_NAME}/
RUN cat ~/.alias >> ~/.bashrc &&\
    rm .alias
