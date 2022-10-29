FROM ubuntu:22.04

LABEL author="Joe Purdy <joe@purdy.dev>"

# Install locales
RUN apt-get update && apt-get install -y locales
RUN locale-gen en_US.UTF-8

ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8
ENV TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Get latest version of software-properties-common first
RUN apt-get update && apt-get upgrade -y && apt-get install -y software-properties-common apt-transport-https

# Pre-add php8 repo
RUN add-apt-repository -y ppa:ondrej/php \
    && apt-get update

# Basic Requirements
RUN apt-get update \
    && apt-get install -y nginx curl unzip git supervisor wget python-pip sqlite3

# PHP Requirements
RUN apt-get update \
    && apt-get install -y php8.1 php8.1-fpm php8.1-cli php8.1-mcrypt php8.1-gd php8.1-mysql \
    php8.1-imap php-memcached php8.1-mbstring php8.1-xml php8.1-curl \
    php8.1-sqlite3

# Wordpress Requirements
RUN apt-get update \
    && apt-get install -y libnuma-dev php8.1-intl php-pear php8.1-imagick \
    php8.1-ps php8.1-pspell php8.1-tidy php8.1-xmlrpc php8.1-xsl

# Install Composer
COPY --from=composer/composer /usr/bin/composer /usr/bin/composer

# Install WP-CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp

# Misc. Cleanup
RUN mkdir /run/php \
    && apt remove -y --purge software-properties-common \
    && apt -y autoremove \
    && apt clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf \
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

COPY default /etc/nginx/sites-available/default
COPY php-fpm.conf /etc/php/8.1/fpm/php-fpm.conf

EXPOSE 80

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]