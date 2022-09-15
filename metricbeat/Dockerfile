FROM centos:8

ARG RESTY_IMAGE_BASE="jim-java-env"
ARG RESTY_IMAGE_TAG="1.0"

# 安装过程中如果中途有错误会自动中止，只要重新再执行一遍就可以了

#构建参数
#ARG RESTY_VERSION="1.19.3.1"

LABEL MAINTAINER "yourname@gmail.com"

#工作路径，所有工作文件都放这里
WORKDIR /data

RUN yum clean all
RUN yum makecache

RUN yum install -y wget sudo telnet net-tools glibc.i686
#创建用户和组
RUN mkdir -p /data && \
    chmod a+w /data && \
    groupadd -g 1000 www && \
    useradd -g 1000 -u 1000 www && \
    echo "www  ALL = ( ALL ) NOPASSWD: ALL" >> /etc/sudoers && \
    chown -R www:www /data

#解压缩jdk并搭建环境
RUN echo "开始创建jdk目录"
RUN mkdir -p /usr/lib/jvm -p
ADD files/jdk.tar.gz /usr/lib/jvm
RUN ln $(ls /usr/lib/jvm)  /usr/lib/jvm/jdk -s
RUN ln /usr/lib/jvm/jdk/bin/java /usr/bin/java -s
RUN ln /usr/lib/jvm/jdk/bin/jps /usr/bin/jps -s
RUN ln /usr/lib/jvm/jdk/bin/jhat /usr/bin/jhat -s
RUN ln /usr/lib/jvm/jdk/bin/jmap /usr/bin/jmap -s

#配置环境变量，并加入到全局变量
ENV JAVA_HOME /usr/lib/jvm/jdk
ENV PATH $JAVA_HOME/bin:$PATH

STOPSIGNAL SIGQUIT

#定义开放的端口
#EXPOSE ${EXPORT_PORTS}
#CMD [${AUTO_RUN_COMMAND}]
