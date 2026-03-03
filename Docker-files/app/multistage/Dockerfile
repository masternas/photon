FROM eclipse-temurin:11-jdk AS BUILD_IMAGE
RUN apt update && apt install maven git -y
# We clone it into a directory named 'photon'
RUN git clone https://github.com/masternas/photon.git
# We enter 'photon' to build the app
RUN cd photon && git checkout docker && mvn install

FROM tomcat:9-jre11
RUN rm -rf /usr/local/tomcat/webapps/*

# FIX: Change 'vprofile-project' to 'photon' to match the folder above
COPY --from=BUILD_IMAGE photon/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]

