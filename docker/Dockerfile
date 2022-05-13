FROM ansiblesemaphore/semaphore:latest

USER root

ENV LD_LIBRARY_PATH=/lib:/lib/oracle/11.2/client64/lib
ENV ORACLE_HOME=/lib/oracle/11.2/client64

RUN apk add curl bash python3-dev py3-pip py3-virtualenv procps lapack libstdc++ g++ gcc gfortran musl-dev lapack-dev libaio libnsl

RUN curl -k -o /tmp/basic.zip https://raw.githubusercontent.com/wilo087/Oracle-Instaclient_11_2/master/instantclient-basic-linux.x64-11.2.0.4.0.zip

# Unzip downloaded library
RUN unzip -d /tmp/oracle/ /tmp/basic.zip

RUN mkdir -p /lib/oracle/11.2/client64/lib && \
    cp /tmp/oracle/instantclient_11_2/* /lib/oracle/11.2/client64/lib/ && \
    rm -rf /tmp/oracle

RUN ln -s /lib/oracle/11.2/client64/lib/libclntsh.so.11.1 /lib/oracle/11.2/client64/lib/libclntsh.so
RUN ln -s /usr/lib/libnsl.so.2.0.1 /lib/libnsl.so.1

COPY requirements.txt /tmp/requirements.txt
RUN pip3 install -r /tmp/requirements.txt
RUN rm /tmp/requirements.txt

COPY requirements.yml /tmp/requirements.yml
RUN ansible-galaxy install -r /tmp/requirements.yml
RUN rm /tmp/requirements.yml

WORKDIR /home/semaphore
USER 1001

