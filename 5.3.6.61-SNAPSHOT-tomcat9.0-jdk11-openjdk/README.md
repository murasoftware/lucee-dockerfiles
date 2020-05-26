# build lucee image
docker build -t blueriver/lucee:5.3.5.78-RC-tomcat9.0-jdk11-openjdk .

# build mura standard image
docker build -t blueriver/mura:7.1.#PUT_LATEST_VERSION_OF_MURA_HERE#-lucee5.3.5.78-RC-tomcat9.0-jdk11-openjdk  -f core/docker/build-5.3.5.78-RC-tomcat9.0-jdk11-openjdk/Dockerfile .

# build custom for project image
docker build -t blueriver/mura:7.1.477.custom.1-lucee5.3.5.78-RC-tomcat9.0-jdk11-openjdk  -f core/docker/build-5.3.5.78-RC-tomcat9.0-jdk11-openjdk/Dockerfile .
