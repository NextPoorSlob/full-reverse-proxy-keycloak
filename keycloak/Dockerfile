#Dockerfile contents START

FROM quay.io/keycloak/keycloak:23.0.4

# Copy the contents from the "builder" stage to the current stage
COPY cert/ /opt/keycloak/conf/

# Configure a database vendor
ENV KC_DB=postgres
ENV KC_DB_USERNAME=postgres
ENV KC_DB_PASSWORD=keycloak
ENV KC_DB_URL=jdbc:postgresql://database:5432/postgres

ENV KEYCLOAK_ADMIN=admin
ENV KEYCLOAK_ADMIN_PASSWORD=admin

ENV KC_HEALTH_ENABLED true
ENV KC_HTTP_PORT 8080
ENV KC_HTTPS_PORT 8443

# Set the entry point for the container to "/opt/keycloak/bin/kc.sh"
# 10.xx.yy.zz is IP of machine which is running the container
ENTRYPOINT ["/opt/keycloak/bin/kc.sh", "start", \
"--https-port=${KC_HTTPS_PORT}", \
"--http-port=${KC_HTTP_PORT}", \
"--https-key-store-file=/opt/keycloak/conf/keycloak.keystore.p12", \
"--https-key-store-password=keycloak", \
"--https-key-store-type=PKCS12", \
"--hostname=keycloak", \
"--hostname-admin=admin.keycloak"]

#Dockerfile contents END
