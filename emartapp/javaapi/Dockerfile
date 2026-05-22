FROM eclipse-temurin:8-jdk-alpine AS BUILD_IMAGE

WORKDIR /usr/src/app/

# Instalează maven
RUN apk add --no-cache maven

# Copiază și build
COPY ./ /usr/src/app/
RUN mvn install -DskipTests

# Etapa runtime (mai mică)
FROM eclipse-temurin:8-jre-alpine

WORKDIR /usr/src/app/

# Copiază jar-ul din etapa de build
COPY --from=BUILD_IMAGE /usr/src/app/target/book-work-0.0.1-SNAPSHOT.jar ./book-work-0.0.1.jar

EXPOSE 9000
ENTRYPOINT ["java", "-jar", "book-work-0.0.1.jar"]