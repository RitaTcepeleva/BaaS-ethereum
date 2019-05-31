FROM ubuntu:16.04

ENV DEBIAN_FRONTEND=noninteractive

EXPOSE 3000

RUN apt-get update && apt-get install --yes bash
RUN apt-get update && apt-get install --yes docker
RUN apt-get update && apt-get install --yes python
RUN apt-get update && apt-get install --yes software-properties-common
RUN add-apt-repository ppa:ethereum/ethereum
RUN apt-get update && apt-get install --yes geth

RUN apt-get update && apt-get install --yes net-tools
RUN apt-get update && apt-get install --yes curl
RUN apt-get update && apt-get install --yes iputils-ping

RUN apt-get update && apt-get install --yes nodejs
RUN apt-get update && apt-get install --yes nodejs npm
RUN apt-get update && apt-get install --yes npm
RUN apt-get update && apt-get install --yes git
RUN curl -O "https://storage.googleapis.com/golang/go1.11.2.linux-amd64.tar.gz"
RUN tar -xvf "go1.11.2.linux-amd64.tar.gz"
RUN mv go /usr/local
RUN export GOPATH=$HOME/home/eth_user/
RUN export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin
RUN export GOROOT=$HOME/go

RUN curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

RUN cd /root && git clone https://github.com/cubedro/eth-net-intelligence-api && cd eth-net-intelligence-api &&  npm install && npm install -g pm2
#RUN npm install web3
#ADD app.json /root/eth-net-intelligence-api/app.json
RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN adduser --disabled-login --gecos "" eth_user

COPY eth_common /home/eth_user/eth_common
RUN chown -R eth_user:eth_user /home/eth_user/eth_common

#USER eth_user

WORKDIR /home/eth_user
#RUN geth init eth_common/genesis.json
RUN geth --datadir /home/eth_user --networkid="51" init eth_common/genesis.json
#RUN geth --rpc --ws --rpcapi="eth,web3,personal" --wsorigins="*" --wsapi="eth,web3,personal"


ENTRYPOINT bash

#RUN add-apt-repository ppa:webupd8team/atom
#RUN apt-get update
#RUN apt-get install -y  atom

#RUN apm install etheratom
#RUN geth --rpc --ws --rpcapi="eth,web3,personal" --wsorigins="*" --wsapi="eth,web3,personal"
RUN curl https://install.meteor.com/ | sh
RUN git clone http://github.com/SilentCicero/meteor-dapp-cosmo.git
RUN cd meteor-dapp-cosmo/app
WORKDIR /home/eth_user/meteor-dapp-cosmo/app/
#RUN curl https://install.meteor.com/ | sh
#RUN meteor create myapp --allow-superuser
#RUN cd myapp/
#CMD sh -c "docker run -p 3000:3000"
CMD [" meteor --allow-superuser","-h","localhost:3000"]


