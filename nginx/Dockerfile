# 基礎鏡像
FROM centos

# 維護者
MAINTAINER 271648298@qq.com

# 安裝wget下載工具
RUN yum install -y wget 

# 切換到usr/lcoal/src/目錄，相當於cd，並可以用cd 代替， 但docker官方不建議用cd
WORKDIR /usr/local/src

# 添加遠程文件到當前文件夾， 注意：後面有個點(.) 代表當前目錄。 ADD可以添加遠程文件到鏡像，但COPY僅可以添加本地文件到鏡像中。
ADD http://nginx.org/download/nginx-1.17.0.tar.gz .

# RUN，在鏡像內運行解壓命令
RUN tar zxvf nginx-1.17.0.tar.gz

# 切換目錄
WORKDIR /usr/local/src/nginx-1.17.0

# 更新yum，可不執行
# RUN yum -y update 

# 安裝必要的軟件和添加nginx用戶
RUN yum install -y gcc gcc-c++ glibc make openssl-devel
RUN yum install -y libxslt-devel -y gd-devel GeoIP GeoIP-devel pcre pcre-devel
RUN  useradd -M -s /sbin/nologin nginx

# 掛載卷，測試用例（這裡的掛載卷，不可以指定本機的目錄，不夠靈活，一般會在 啟動容器時通過 -v 參數指定掛載卷，或在docker-compose.yaml文件中指定，都可以指定本地目錄）
VOLUME ["/data"]

# 編譯安裝nginx
RUN ./configure --user=nginx --group=nginx --prefix=/usr/local/nginx --with-file-aio --with-http_ssl_module --with-http_realip_module --with-http_addition_module --with-http_xslt_module --with-http_image_filter_module --with-http_geoip_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_degradation_module --with-http_stub_status_module && make && make install

# 切換到Nginx的配置目錄
WORKDIR /usr/local/nginx/conf

# 建立子配置文件夾，個人愛好，可以不建，或者叫其它名稱都可以，但最好不要帶特殊符號,
RUN mkdir vhost


# 設置變量，執行命令時，就可以省略前綴目錄了	
ENV PATH /usr/local/nginx/sbin:$PATH


# 暴露端口
EXPOSE 80

# 入口點命令
ENTRYPOINT ["nginx"]

# 執行命令，數組形式， "-g daemon off;" 使我們運行容器時，容器可以前台運行，不會退出
CMD ["-g", "daemon off;"]