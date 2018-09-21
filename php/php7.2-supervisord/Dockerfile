FROM php:7.2-cli
# APT 自动安装 PHP 相关的依赖包,如需其他依赖包在此添加
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        freetds-dev \
        libicu-dev \
        libpq-dev \
        supervisor \
    && docker-php-ext-install -j$(nproc) iconv pdo_mysql mbstring intl pcntl zip \
    # 用完包管理器后安排打扫卫生可以显著的减少镜像大小
    && apt-get clean \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \

# 配置默认放置 App 的目录
RUN mkdir -p /app

WORKDIR /app

RUN usermod -u 1000 www-data

# Default command
CMD ["/usr/bin/supervisord"]