ARG BASE_IMAGE=nvcr.io/nvidia/pytorch:22.04-py3
FROM ${BASE_IMAGE}

ARG PROJECT_NAME=ascender
ARG USER_NAME=challenger
ARG APPLICATION_DIRECTORY=/home/${USER_NAME}/${PROJECT_NAME}

ENV DEBIAN_FRONTEND="noninteractive" \
    LC_ALL="C.UTF-8" \
    LANG="C.UTF-8" \
    PYTHONPATH=${APPLICATION_DIRECTORY}

RUN pip3 install poetry

# Add user. Without this, following process is executed as admin. 
RUN useradd -ms /bin/sh ${USER_NAME}
USER ${USER_NAME}

WORKDIR ${APPLICATION_DIRECTORY}
COPY pyproject.toml .
COPY poetry.lock .
RUN poetry install

ENTRYPOINT ["jupyter", "lab", "--allow-root", "--ip=0.0.0.0", "--port=6060", "--no-browser"]