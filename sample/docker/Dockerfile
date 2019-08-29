FROM maven:3.6 AS sample-build

ARG REPO_PATH

WORKDIR /build/temp

COPY ./ /build/temp

RUN echo '### Build components' \
    && mvn clean install -f $REPO_PATHhello

FROM adoptopenjdk/openjdk11:alpine AS test-image

WORKDIR /app

COPY --from=payer-ott-gateway-build \
    /build/temp/target/cc-sample-1.0-SNAPSHOT-jar-with-dependencies.jar \
    /app/cc-sample.jar

ENTRYPOINT ["sh", "-c", "java -jar /app/cc-sample.jar"]
