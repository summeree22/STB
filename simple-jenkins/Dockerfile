
# Jenkin 이미지를 생성할때 기반이 되는 베이스 이미지 지정
FROM jenkins/jenkins:lts

# 루트 계정으로 전환
USER root

SHELL ["/bin/bash", "-c"]

# Jenkin 이미지 내 모든 패키지와 의존성 설치 
RUN apt-get update && \
    apt-get install -y ca-certificates curl gnupg lsb-release && \
    mkdir -m 0755 -p /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    apt-get update && \
    apt-get install -y docker-ce docker-ce-cli containerd.io && \
    usermod -aG docker jenkins && \
    # Docker Compose 최신 버전 다운로드 및 설치
    curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose && \
    ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

# 일반 사용자 계정으로 전환
USER jenkins