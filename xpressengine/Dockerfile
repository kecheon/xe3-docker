# --------------------------------------------------
#  Dockerfile for installing XpressEngine 3
# --------------------------------------------------

# FROM php:7.3-apache
FROM debian:buster

ARG USER_ID
ARG GROUP_ID

MAINTAINER Sunggun Yu <sunggun.dev@gmail.com>

# Install required packages
RUN set -x \
    && apt-get update \
    && apt-get install -y \
    sudo \
    wget \
    unzip \
    ca-certificates \
    apt-transport-https \
    git \
    zlib1g-dev \
    libpng-dev \
    libcurl4-openssl-dev \
    python python-pip \
    openssl \
    apache2 \
    php \
    php-common \
    php-cli \
    php-fpm php-json php-pdo php-mysql php-zip php-gd  php-mbstring php-curl php-xml php-pear php-bcmath \
    php-curl php-fileinfo php-mbstring libapache2-mod-php \
    libcap2-bin procps
 #   python-pip \
 #   gnupg

# Install required PHP extensions for XpressEngine
# RUN set -x \
#     && docker-php-ext-install mbstring tokenizer curl pdo_mysql fileinfo

# Enableing the Apache2 rewrite module
RUN set -x \
    && a2enmod rewrite

# Install jinja2-cli for templating the `.xe_install_config.yaml` file
RUN set -x \
    && pip install --no-cache-dir jinja2-cli

# Cleanup
RUN set -x \
    && rm -rf /var/lib/apt/lists/*


# COPY ./xpressengine/files/* /var/www/html/
# install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
# RUN HASH="$(wget -q -O - https://composer.github.io/installer.sig)"
# RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN setcap 'cap_net_bind_service=+ep' /usr/sbin/apache2
WORKDIR /var/www/html
RUN addgroup --gid $GROUP_ID ubuntu
RUN adduser --disabled-password --gecos '' --uid $USER_ID --gid $GROUP_ID ubuntu
RUN chown -R $USER_ID:$GROUP_ID /var/www/html
RUN chown -R $USER_ID:$GROUP_ID /var/run/apache2
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER ubuntu

ENTRYPOINT ["/var/www/html/entrypoint.sh"]

# CMD ["apache2-foreground"]
CMD ["/usr/sbin/apache2ctl", "-DFOREGROUND"]
# CMD ["apache2ctl","-D","FOREGROUND"]

