FROM softleader/build-env:jcconf2018 As build-env
WORKDIR /app
ADD . /app
RUN mvn clean package -DskipTests

FROM openjdk:8-jre-alpine
RUN apk update \
 && apk --no-cache add git tzdata \
 && ls /usr/share/zoneinfo \
 && cp /usr/share/zoneinfo/Asia/Taipei /etc/localtime  \
 && rm -rf /var/cache/apk/*

VOLUME /tmp

COPY config /config
COPY entrypoint.sh /entrypoint.sh
COPY --from=build-env /app/target/app.jar /app.jar

ENTRYPOINT ["/bin/sh", "/entrypoint.sh"]
