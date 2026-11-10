# ==========================================
# STAGE 1: Kacha Maal Pakanay Ka Hissa (Build)
# ==========================================
FROM maven:3.8.4-openjdk-11 AS build
WORKDIR /app

# Factory (Maven) ko rulebook aur code dena
COPY pom.xml .
COPY src ./src

# Factory chala kar code ko .war file mein pack karna
RUN mvn clean package -DskipTests

# ==========================================
# STAGE 2: App Chalane Ka Hissa (Production/Tomcat)
# ==========================================
FROM tomcat:9.0-jdk11-openjdk-slim

# Security ke liye default kachra saaf karna
RUN rm -rf /usr/local/tomcat/webapps/*

# Stage 1 se bani hui .war file ko Tomcat (Engine) mein lana
COPY --from=build /app/target/*.war /usr/local/tomcat/webapps/ROOT.war

# Port 8080 open karna taake bahar se traffic aa sake
EXPOSE 8080

# Tomcat server start karna
CMD ["catalina.sh", "run"]
