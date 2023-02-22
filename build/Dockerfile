FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y wget gcc build-essential libssl-dev net-tools liblzo2-dev libpam0g-dev

# download binary openssl packages from Impish builds
RUN wget http://security.ubuntu.com/ubuntu/pool/main/o/openssl/openssl_1.1.1f-1ubuntu2.17_amd64.deb
RUN wget http://security.ubuntu.com/ubuntu/pool/main/o/openssl/libssl-dev_1.1.1f-1ubuntu2.17_amd64.deb
RUN wget http://security.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.17_amd64.deb

# install downloaded binary packages
RUN dpkg -i libssl1.1_1.1.1f-1ubuntu2.17_amd64.deb
RUN dpkg -i libssl-dev_1.1.1f-1ubuntu2.17_amd64.deb
RUN dpkg -i openssl_1.1.1f-1ubuntu2.17_amd64.deb

RUN rm -f *.deb

RUN wget https://swupdate.openvpn.org/community/releases/openvpn-2.4.7.tar.gz
RUN tar xfz openvpn-2.4.7.tar.gz
WORKDIR openvpn-2.4.7
RUN ./configure
RUN make
RUN make install
WORKDIR ../
RUN rm openvpn-2.4.7.tar.gz

COPY . /usr/local/bin

ENV KILL_SWITCH=on

ENTRYPOINT [ "entry.sh" ]
