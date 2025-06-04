FROM rocm/pytorch:latest

ARG REMOTE_USER
ARG REMOTE_UID
ARG REMOTE_GID
RUN <<EOF
    addgroup --gid ${REMOTE_GID} ${REMOTE_USER}
    adduser --disabled-password --uid ${REMOTE_UID} --gid ${REMOTE_GID} ${REMOTE_USER}
EOF

ENV HOME /home/${REMOTE_USER}

USER ${REMOTE_USER}

ARG VENV_PATH=/opt/dev-venv
ENV VENV_ACTIVATE=${VENV_PATH}/bin/activate
ENV DEBIAN_FRONTEND="noninteractive"

RUN apt update

# install OpenCV to test compilation with external libraries
RUN apt install -y libopencv-dev pkg-config

# make & language-pack-en are for documentation
RUN apt install -y \
    git \
    language-pack-en \
    make \
    python3-venv \
    openssh-client

# we create the virtualenv here so that the devcontainer.json setting
# python.defaultInterpreterPath can be used to find it; if we do it in the
# post_create.sh script, the virtualenv will not be loaded and features like
# pylance, black, isort, etc. will not work
RUN python3 -m venv ${VENV_PATH}
RUN echo "source ${VENV_ACTIVATE}" >> ~/.bashrc

#RUN pip install -e .[dev]
#RUN echo "hipconfig" >> ~/.bashrc
