FROM ubuntu:latest

ENV DEBIAN_FRONTEND=nointeractive

RUN apt update \
 && apt upgrade -y \
 && apt install -y --no-install-recommends curl ca-certificates

RUN useradd --create-home --user-group guest \
 && echo -n 'guest:guest' | chpasswd

RUN update-ca-certificates \
 && curl https://deb.releases.teleport.dev/teleport-pubkey.asc -o /usr/share/keyrings/teleport-archive-keyring.asc \
 && echo "deb [signed-by=/usr/share/keyrings/teleport-archive-keyring.asc] https://deb.releases.teleport.dev/ stable main" \
  | tee /etc/apt/sources.list.d/teleport.list > /dev/null \
 && apt update \
 && apt install -y teleport

ADD ./teleport.yaml /etc/teleport.yaml

CMD /usr/local/bin/teleport start --config=/etc/teleport.yaml --pid-file=/run/teleport.pid

