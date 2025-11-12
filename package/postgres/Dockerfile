# 使用镜像
FROM postgres:latest

COPY ./extension/ /tmp/extensions

# 生产环境
RUN apt update && apt install -y gcc make llvm-19-dev \
    && cd /tmp/extensions/pgvector && make && make install \
    && cd /tmp/extensions/scws-1.2.3 && make && make install \
    && cd /tmp/extensions/zhparser && make && make install

# 开发环境(方便调试，建议使用生产环境，构建docker镜像缓存层更少，体积更小)
# RUN apt update && apt install -y gcc make llvm-19-dev
# RUN cd /tmp/extensions/pgvector && make && make install
# RUN cd /tmp/extensions/scws-1.2.3 && make && make install
# RUN cd /tmp/extensions/zhparser && make && make install
# RUN psql -U postgres -f /tmp/extensions/init_extension.sql
