FROM maven:3.6 AS payer-ott-gateway-build

ARG PROFILE
ARG SERVERPORT

WORKDIR /build/temp

COPY ./ /build/temp

RUN echo '### Build components' \
    && mvn clean install -f hello

FROM adoptopenjdk/openjdk11:alpine AS test-image

WORKDIR /app

COPY --from=payer-ott-gateway-build \
    /build/temp/target/cc-sample-1.0-SNAPSHOT-jar-with-dependencies.jar \
    /app/cc-sample.jar

ENTRYPOINT ["sh", "-c", "java -jar /app/cc-sample.jar"]
