# 操作系统Debian12
FROM python:3.12

ENV PYTHONUNBUFFERED 1
LABEL authors="Oatelauser"

RUN sed -i 's|http://[^/]*|https://mirrors.aliyun.com|g' /etc/apt/sources.list.d/debian.sources \
    && sed -i 's|https://security.debian.org|https://mirrors.aliyun.com/debian-security|g' /etc/apt/sources.list.d/debian.sources \
    && apt update \
    && apt install -y openssh-server \
    && mkdir /var/run/sshd \
    # 设置SSH账户密码
    && echo 'root:root' | chpasswd \
    && sed -i 's/\#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && apt clean autoclean \
    && apt autoremove -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/log/*.log


EXPOSE 22
ENTRYPOINT ["/usr/sbin/sshd", "-D"]