FROM gradle

RUN apt-get update \
    && apt-get -y install curl \
    && apt-get -y install build-essential 

RUN echo gcc version "\n$(gcc --version)"

CMD [ "tail", "-f /dev/null" ]