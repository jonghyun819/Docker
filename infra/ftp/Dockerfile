# 1단계: 빌드 - vsftpd와 필수 패키지만 /rootfs에 설치
FROM quay.io/centos/centos:stream10 AS builder
RUN dnf -y --installroot=/rootfs --releasever=10 \
        --setopt=install_weak_deps=False --setopt=tsflags=nodocs \
        install vsftpd \
    && dnf --installroot=/rootfs clean all
COPY vsftpd.conf.template /rootfs/etc/vsftpd/vsftpd.conf
COPY WelcomeToFTP.txt /rootfs/var/ftp/pub/

# 2단계: 실행 - 빈 이미지에 /rootfs만 복사
FROM scratch
LABEL maintainer="team" description="FTP server (ftp.example.com)"
COPY --from=builder /rootfs /
VOLUME /var/ftp/pub
EXPOSE 21/tcp
EXPOSE 20/tcp
ENTRYPOINT ["/usr/sbin/vsftpd"]
