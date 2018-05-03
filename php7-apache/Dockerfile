FROM php:7.1-apache
MAINTAINER lixiaomin <xiao345@gmail.com>
# APT 自动安装 PHP 相关的依赖包,如需其他依赖包在此添加
RUN apt-get update \
    && apt-get install -y \
    libmcrypt-dev \
    libz-dev \
    git \
    wget \
    python \
    curl \
    supervisor \
    cron \
    vim \
    yarn \
    # 官方 PHP 镜像内置命令，安装 PHP 依赖
    && docker-php-ext-install \
    pcntl \
    mcrypt \
    mbstring \
    pdo_mysql \
    zip \
    # 用完包管理器后安排打扫卫生可以显著的减少镜像大小
    && apt-get clean \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    # 安装 Composer，此物是 PHP 用来管理依赖关系的工具
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -L http://peak.telecommunity.com/dist/ez_setup.py | python -
# RUN easy_install supervisor
# RUN echo_supervisord_conf > /etc/supervisord.conf
# RUN echo "[include]" >> /etc/supervisord.conf
# RUN echo "files = /etc/supervisord.d/*.ini" >> /etc/supervisord.conf
# RUN mkdir /etc/supervisord.d

# Composer中国全量镜像
RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com

# 开启 URL 重写模块
# 配置默认放置 App 的目录
RUN a2enmod rewrite \
    && mkdir -p /app \
    && rm -fr /var/www/html \
    && ln -s /app/public /var/www/html
RUN chown -R www-data:www-data /app
# RUN chmod -R 0777 /app

#COPY supervisord.conf /etc/supervisord.conf
#ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisord.conf"]

WORKDIR /app