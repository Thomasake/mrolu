FROM openjdk:latest AS BUILD_IMAGE
WORKDIR /usr/src/app/
#RUN apt update && yum install maven -y
#RUN choco install maven -y
FROM alpine:latest
RUN apk add --no-cache wget ca-certificates
RUN wget https://apache.mirrors.benatherton.com/maven/maven-3/3.8.3/binaries/apache-maven-3.8.3-bin.tar.gz && \
    tar -xzf apache-maven-3.8.3-bin.tar.gz && \
    rm apache-maven-3.8.3-bin.tar.gz
RUN mv apache-maven-3.8.3 /opt/maven && \
    ln -s /opt/maven/bin/mvn /usr/bin/mvn

COPY ./ /usr/src/app/
RUN mvn install -DskipTests

FROM openjdk:latest

WORKDIR /usr/src/app/
COPY --from=BUILD_IMAGE /usr/src/app/target/book-work-0.0.1-SNAPSHOT.jar ./book-work-0.0.1.jar

EXPOSE 9000
ENTRYPOINT ["java","-jar","book-work-0.0.1.jar"]
# Test