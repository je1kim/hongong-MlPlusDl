# 기반 이미지 불러오기
FROM centos:7.9.2009

# 필요 패키지 설치
RUN yum install -y gcc \
                   openssl-devel \
                   bzip2-devel \
                   libfii-devel \
                   openssh-server \
                   openssh-clients \
                   vim-enhanced \
                   net-tools \
                   tar \
                   unzip \
                   git \
                   wget \
                   curl

# KST(Asia/Seoul) 시간대로 설정
RUN ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime

# LANG 설정(언어 설정)
RUN localedef -f UTF-8 -i ko_KR ko_KR.utf8
ENV LANG=ko_KR.utf8
ENV LC_LANG=ko_KR.utf8

# 컨테이너 내부에 사용할 포트 노출
EXPOSE 20 21 22 80 3306 1521 8888

# ROOT 사용자 설정
RUN echo 'root:root' | chpasswd

# USER 계정 설정
RUN useradd -m usr01
RUN echo 'usr01:usr01' | chpasswd

# miniconda 다운로드>설치>환경설정
# Python version 3.11
RUN wget --no-check-certificate https://repo.anaconda.com/miniconda/Miniconda3-py311_23.11.0-2-Linux-x86_64.sh
RUN sh Miniconda3-py311_23.11.0-2-Linux-x86_64.sh -b -p /opt/miniconda3
RUN rm -rf Miniconda3-py311_23.11.0-2-Linux-x86_64.sh

ENV PATH="/opt/miniconda3/bin:${PATH}"

# Python 가상환경 패키지 다운로드
#RUN pip install pipenv

# SSH 서비스 활성화
RUN systemctl enable sshd

CMD ["/usr/sbin/init"]
