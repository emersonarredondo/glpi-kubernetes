#On choisit une debian
FROM debian:11.1

LABEL org.opencontainers.image.authors="emerson@arredondo.pe"

ENV DEBIAN_FRONTEND noninteractive

#Install dependencies 
RUN apt update \
&& apt install --yes --no-install-recommends \
apache2 \
php7.4 \
php7.4-mysql \
php7.4-ldap \
php7.4-xmlrpc \
php7.4-imap \
curl \
php7.4-curl \
php7.4-gd \
php7.4-mbstring \
php7.4-xml \
php7.4-apcu-bc \
php-cas \
php7.4-intl \
php7.4-zip \
php7.4-bz2 \
cron \
nano \
wget \
ca-certificates \
jq \
libldap-2.4-2 \
libldap-common \
libsasl2-2 \
libsasl2-modules \
libsasl2-modules-db \
&& rm -rf /var/lib/apt/lists/*

#Copy Script  and install glpi 
COPY glpi-start.sh /opt/
RUN chmod +x /opt/glpi-start.sh
ENTRYPOINT ["/opt/glpi-start.sh"]

#Expose ports
EXPOSE 80 
