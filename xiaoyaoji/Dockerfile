FROM tomcat
MAINTAINER lixiaomin <xiao345@gmail.com>
WORKDIR /tmp
RUN wget https://github.com/zhoujingjie/xiaoyaoji/releases/download/v2.1.5.1/xiaoyaoji-2.1.5.1.zip && \
    mv xiaoyaoji-2.1.5.1.zip /usr/local/tomcat/webapps/ROOT/xiaoyaoji-2.1.5.1.zip \
WORKDIR /usr/local/tomcat/webapps/ROOT
RUN unzip xiaoyaoji-2.1.5.1.zip && \
    rm -f xiaoyaoji-2.1.5.1.zip && \