##########
## BASE ##
##########

FROM ubuntu:latest

ENV PYTHONUNBUFFERED=1

# SYSTEM
RUN apt-get update --yes --quiet && DEBIAN_FRONTEND=noninteractive apt-get install --yes --quiet --no-install-recommends \
    software-properties-common openssh-client \
    build-essential ca-certificates

# PYTHON 3.10
RUN DEBIAN_FRONTEND=noninteractive apt-get update --yes --quiet && \
    apt-get install --yes --quiet \
        python3.10 \
        python3.10-dev \
        python3.10-distutils \
        pip \
    && rm -rf /var/lib/apt/lists/*

############
## SERVER ##
############

ENV APP_HOME /app
WORKDIR $APP_HOME
RUN \
    pip install --upgrade poetry && \
    poetry config virtualenvs.create false && \
    poetry config installer.max-workers 10

COPY ./requirements.txt $APP_HOME/

RUN pip install -r requirements.txt

COPY ./ $APP_HOME/

CMD [ \
    "jupyter", "lab", \
    "--ip", "0.0.0.0", "--port", "8888", \
    "--allow-root", "--no-browser", "--NotebookApp.token=''", "--NotebookApp.password=''" \
]
