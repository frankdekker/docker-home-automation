FROM ghcr.io/home-assistant/amd64-base-python:latest

RUN apk add --no-cache git

RUN pip install git+https://github.com/gabrielwong159/wyoming-stt-api.git@v2.0.0

COPY run.sh /
RUN chmod a+x /run.sh

CMD ["/run.sh"]
