FROM openjdk:latest AS BUILD_IMAGE
WORKDIR /usr/src/app/
#RUN apt update && yum install maven -y
#RUN choco install maven -y
RUN wget http://security.ubuntu.com/ubuntu/pool/main/a/apt/apt_2.0.2ubuntu0.2_amd64.deb --2022-11-14 10:09:15--  http://security.ubuntu.com/ubuntu/pool/main/a/apt/apt_2.0.2ubuntu0.2_amd64.deb
RUN sudo dpkg -i apt_2.0.2ubuntu0.2_amd64.deb
RUN sudo apt-get update && sudo apt-get install maven -y
COPY ./ /usr/src/app/
RUN mvn install -DskipTests

FROM openjdk:latest

WORKDIR /usr/src/app/
COPY --from=BUILD_IMAGE /usr/src/app/target/book-work-0.0.1-SNAPSHOT.jar ./book-work-0.0.1.jar

EXPOSE 9000
ENTRYPOINT ["java","-jar","book-work-0.0.1.jar"]
# Test