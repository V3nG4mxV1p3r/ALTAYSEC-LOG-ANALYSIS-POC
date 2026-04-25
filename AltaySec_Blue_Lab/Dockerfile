FROM ubuntu:22.04

RUN apt-get update && apt-get install -y wget curl nano grep gawk && \
    wget https://github.com/yudai/gotty/releases/download/v1.0.1/gotty_linux_amd64.tar.gz && \
    tar -zxvf gotty_linux_amd64.tar.gz && \
    mv gotty /usr/local/bin/ && \
    rm gotty_linux_amd64.tar.gz

WORKDIR /home/analyst

COPY access.log /home/analyst/access.log
RUN echo "LEVEL 1: RECON & BRUTE FORCE \n\nGOREV: access.log dosyasini incele. \n1- /admin/login.php sayfasina yonelik POST isteklerini (Brute Force) bul. \n2- Basarili olan girisi (HTTP 302) tespit et. \n\nFlag, basarili olan log satirinin (User-Agent kisminin) icinde gizlidir!" > gorev.txt

EXPOSE 80

CMD ["gotty", "-w", "-p", "80", "bash"]
