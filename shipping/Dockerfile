FROM alpine:latest AS build
RUN apk add --no-cache \
    openjdk17 \
    maven \
    bash
RUN addgroup -r shipping && adduser -r -m -g shipping shipping
WORKDIR /opt/shipping
RUN chown -R shipping:shipping /opt/shipping
USER shipping
COPY pom.xml /opt/shipping/
RUN mvn dependency:resolve
COPY src /opt/shipping/src/
RUN mvn package

FROM openjdk:8-jre-alpine
EXPOSE 8080
WORKDIR /opt/shipping
ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql
COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar
CMD [ "java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar" ]

# FROM debian:11 AS build
# RUN apt-get update && \
#     apt-get install -y maven && \
#     apt-get clean && \
#     rm -rf /var/lib/apt/lists/*
# WORKDIR /opt/shipping
# COPY pom.xml /opt/shipping/
# RUN mvn dependency:resolve
# COPY src /opt/shipping/src/
# RUN mvn package

# FROM openjdk:8-jre-alpine
# EXPOSE 8080
# WORKDIR /opt/shipping
# ENV CART_ENDPOINT=cart:8080
# ENV DB_HOST=mysql
# COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar
# CMD [ "java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar" ]