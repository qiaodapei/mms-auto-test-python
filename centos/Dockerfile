FROM centos:centos7.6.1810 
# 镜像的作者 
LABEL maintainer="<371583076@qq.com>" \
      name="jenkins" \
      author="xiao.li" \
      vendor="qiaodapei" \
      version="2.176.2" \
      systemver="centos" \
      desc="mms-auto-test" \
      build-date="20190816"   
COPY Resource /tmp/Resource
### SET ENVIRONNEMENT
ENV LANG=zh_CN.UTF-8 \
    LANGUAGE=zh_CN.UTF-8 \
    TIME_ZONE=Asia/Shanghai 
# Install language pack
RUN localedef -v -c -i en_US -f UTF-8 zh_CN.UTF-8 >/dev/null 2>&1 && \
    grep -q 'zh_CN.utf8' /etc/locale.conf || sed -i -E 's/^LANG=.*/LANG="zh_CN.UTF-8"/' /etc/locale.conf &&\
    yum -y install http://rpms.famillecollet.com/enterprise/remi-release-7.rpm &&\
    yum install -y ntp yum-plugin-fastestmirror vim-enhanced  ntp wget bash-completion elinks lrzsz unix2dos dos2unix java-1.8.0-openjdk openssl openssl-devel \
    git unzip python python-devel net-tools cronie gcc mysql-devel sudo &&\
    yum -y localinstall /tmp/Resource/python37/*.rpm &&ln -s /usr/bin/python37 /usr/bin/python3 &&\
    curl https://bootstrap.pypa.io/get-pip.py -o /tmp/Resource/get-pip.py && python3 /tmp/Resource/get-pip.py &&\
    pip install xlrd xlwt xlsxwriter pymysql xpinyin paramiko redis requests pytest xlutils pandas matplotlib configparser allure-pytest pytest-html openpyxl &&\ 
    cp -r /tmp/Resource/agent.jar /usr/bin/agent.jar && \
    cp -r /tmp/Resource/jenkins.sh /usr/local/bin/jenkins.sh && \
    chmod +x /usr/bin/agent.jar && chmod +x /usr/local/bin/jenkins.sh && \
    ln -sf  /usr/share/zoneinfo/Asia/Shanghai /etc/localtime &&\
    yum clean all && rm -fr /tmp/Resource

WORKDIR /data/jenkins_home


ENTRYPOINT ["/usr/local/bin/jenkins.sh"]
