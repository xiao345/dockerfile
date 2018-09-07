FROM php:7.2
# APT 自动安装 PHP 相关的依赖包,如需其他依赖包在此添加
RUN apt-get update && apt-get install -y \
    libmcrypt-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libxml2-dev \
    && docker-php-ext-install -j$(nproc) iconv pdo_mysql mbstring fileinfo simplexml \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    # 用完包管理器后安排打扫卫生可以显著的减少镜像大小
    && apt-get clean \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    # 安装 Composer，此物是 PHP 用来管理依赖关系的工具
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Composer中国全量镜像
RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com

# install swoole
# RUN pecl install swoole
RUN cd /root/ \
    && git clone https://github.com/swoole/swoole-src.git \
    && cd swoole-src/ \
    && phpize \
    && ./configure \
    && make && make install \
    # && apk del libaio-dev php7-dev git autoconf build-base linux-headers \
    && rm -rf /var/cache/apk/* \
    && rm -rf /root/swoole-src/ \
    && rm -rf /tmp/* \

RUN mkdir -p /app
WORKDIR /app
