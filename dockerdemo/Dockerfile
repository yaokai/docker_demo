# Pull base image  
FROM ubuntu:13.10  
  
MAINTAINER zing wang "zing.jian.wang@gmail.com"  
  
# update source  
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe"> /etc/apt/sources.list  
RUN apt-get update  
  
# Install curl  
RUN apt-get -y install curl  
  
# Install JDK 7  
RUN cd /tmp &&  curl -L 'http://download.oracle.com/otn-pub/java/jdk/8u161-b12/2f38c3b165be4555a1fa6e98c45e0808/jdk-8u161-linux-x64.tar.gz' -H 'Cookie: oraclelicense=accept-securebackup-cookie; gpw_e24=Dockerfile' | tar -xz
RUN mkdir -p /usr/lib/jvm  
RUN mv /tmp/jdk1.8.0_161/ /usr/lib/jvm/java-7-oracle/  
  
# Set Oracle JDK 7 as default Java  
RUN update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-7-oracle/bin/java 300     
RUN update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/java-7-oracle/bin/javac 300     
  
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle/  
  
# Install tomcat7  
RUN cd /tmp && curl -L 'https://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.28/bin/apache-tomcat-8.5.28.tar.gz' | tar -xz  
RUN mv /tmp/apache-tomcat-8.5.28/ /opt/tomcat8/  
  
ENV CATALINA_HOME /opt/tomcat8  
ENV PATH $PATH:$CATALINA_HOME/bin  
  
ADD tomcat8.sh /etc/init.d/tomcat8  
RUN chmod 755 /etc/init.d/tomcat8  
RUN mkdir   /opt/tomcat8/webapps/test && echo "hello world" > /opt/tomcat8/webapps/test/index.html

  
# Expose ports.  
EXPOSE 8080  
  
# Define default command.  
ENTRYPOINT service tomcat8 start && tail -f /opt/tomcat8/logs/catalina.out 