FROM play1docker
RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt yakkety universe" | tee /etc/apt/sources.list.d/groovy.list
RUN { \
  echo 'Package: *'; \
  echo 'Pin: release a=yakkety'; \
  echo 'Pin-Priority: 100'; \
  echo; \
} > /etc/apt/preferences.d/yakkety.pref
RUN apt-get update && \
  apt-get install -y --no-install-recommends -t yakkety libasm-java libjline2-java libqdox-java groovy
