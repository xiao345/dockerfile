FROM php:7.2-apache
# APT 自动安装 PHP 相关的依赖包,如需其他依赖包在此添加
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        freetds-dev \
        libicu-dev \
        libpq-dev \
    && docker-php-ext-install -j$(nproc) iconv pdo_mysql mbstring intl pcntl zip \
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

# 开启 URL 重写模块
# 配置默认放置 App 的目录
RUN a2enmod rewrite \
    && mkdir -p /app \
    && rm -fr /var/www/html

CMD chown -R www-data:www-data /app \
    && ln -s /app/public/* /var/www/html \ 
    && cd /app && composer install  --no-autoloader --no-scripts --no-dev \
    && chmod -R 0777 /app/storage \
    && apache2-foreground

WORKDIR /app
