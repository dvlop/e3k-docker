FROM openjdk:8-alpine

RUN apk --update add --virtual build-dependencies \
    curl \
    && mkdir /embulk \
    && curl -o  /embulk/embulk -L "https://dl.bintray.com/embulk/maven/embulk-$EMBULK_VERSION.jar" \
    && chmod +x /embulk/embulk \
    && apk del build-dependencies

RUN apk --update add libc6-compat

RUN /embulk/embulk gem install embulk-output-elasticsearch
RUN /embulk/embulk gem install embulk-input-mysql
RUN /embulk/embulk gem install embulk-filter-reverse_geocoding

ENTRYPOINT ["sh", "/embulk/embulk"]
