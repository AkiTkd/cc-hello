FROM maven:3.6 AS sample-build

WORKDIR /build/temp

COPY ./ /build/temp

RUN echo '### Build components' \
    && mvn clean install

FROM adoptopenjdk/openjdk11:alpine AS test-image

WORKDIR /app

COPY --from=sample-build \
    /build/temp/target/cc-sample-1.0-SNAPSHOT-jar-with-dependencies.jar \
    /app/cc-sample.jar

ENTRYPOINT ["sh", "-c", "java -jar /app/cc-sample.jar"]
