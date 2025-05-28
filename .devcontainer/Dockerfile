# TODO: use rocm-terminal and build upwards to reduce size
FROM rocm/pytorch:latest

ARG VENV_PATH=/opt/dev-venv
ENV VENV_ACTIVATE=${VENV_PATH}/bin/activate
ENV DEBIAN_FRONTEND="noninteractive"

# install the latest CUDA toolkit (https://developer.nvidia.com/cuda-downloads)
RUN apt update
#RUN echo "PATH=\"\$PATH:/usr/local/cuda/bin\"" >> ~/.bashrc

# install OpenCV to test compilation with external libraries
#RUN apt install -y libopencv-dev pkg-config

# make & language-pack-en are for documentation
RUN apt install -y \
    git \
    language-pack-en \
    make \
    python3-venv
#    gcc \

# we create the virtualenv here so that the devcontainer.json setting
# python.defaultInterpreterPath can be used to find it; if we do it in the
# post_create.sh script, the virtualenv will not be loaded and features like
# pylance, black, isort, etc. will not work
RUN python3 -m venv ${VENV_PATH}
RUN echo "source ${VENV_ACTIVATE}" >> ~/.bashrc

#RUN pip install -e .[dev]
RUN echo "hipconfig" >> ~/.bashrc
