FROM quay.io/keycloak/keycloak:24.0.2 as builder

# Credits to: https://www.linkedin.com/pulse/keycloak-production-setup-aws-ec2-anil-kumar-gurindapalli/

# Enable health and metrics support
ENV KC_HEALTH_ENABLED=true
ENV KC_METRICS_ENABLED=true
ENV KC_FEATURES=token-exchange,admin2,account3,authorization,client-policies,device-flow,scripts

# Configure a database vendor
ENV KC_DB=postgres
ENV KC_DB_URL=jdbc:postgresql://postgres:5432/keycloak
ENV KC_DB_USERNAME=keycloak
ENV KC_DB_PASSWORD=keycloak

ENV KC_HOSTNAME=keycloak
ENV KC_HOSTNAME_DEBUG=true
#ENV KC_HTTPS_PROTOCOLS=TLSv1.3,TLSv1.2
ENV KC_HTTP_PORT=8080
ENV KC_HOSTNAME_STRICT=true
ENV KC_HOSTNAME_STRICT_HTTPS=true
ENV KC_HTTP_ENABLED=true
ENV KC_PROXY=edge

ENV PROXY_ADDRESS_FORWARDING=true
ENV KC_HOSTNAME_STRICT_BACKCHANNEL=true

WORKDIR /opt/keycloak

# for demonstration purposes only, please make sure to use proper certificates in production instead

RUN keytool -genkeypair -storepass password -storetype PKCS12 -keyalg RSA -keysize 2048 -dname "CN=server" -alias server -ext "SAN:c=DNS:localhost,IP:127.0.0.1" -keystore conf/server.keystore
RUN /opt/keycloak/bin/kc.sh build


FROM quay.io/keycloak/keycloak:latest
COPY --from=builder /opt/keycloak/ /opt/keycloak/


#ENTRYPOINT ["/opt/keycloak/bin/kc.sh", "--verbose"]
ENTRYPOINT ["/opt/keycloak/bin/kc.sh"]