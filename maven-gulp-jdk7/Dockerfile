FROM openjdk:7

MAINTAINER Sathwik B P

ENV NODE_VERSION 4.5.0
ENV MAVEN_VERSION 3.3.9
ENV PHANTOSJS_VERSION 2.1.1

ENV WORKSPACE /workspace
ENV PATH /usr/local/bin:$PATH

#install nodejs
RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz" \ 
  && tar -xJf "node-v$NODE_VERSION-linux-x64.tar.xz" -C /usr/local --strip-components=1 \
  && rm "node-v$NODE_VERSION-linux-x64.tar.xz" \
  && ln -s /usr/local/bin/node /usr/local/bin/nodejs

RUN  npm install -g npm@3 \
  && npm install -g minimatch@3.0.2 \
  && npm install -g gulp \
  && npm install -g bower

#install phontomjs
RUN curl -SLO https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-$PHANTOSJS_VERSION-linux-x86_64.tar.bz2 \
  && tar -xf "phantomjs-$PHANTOSJS_VERSION-linux-x86_64.tar.bz2" -C /usr/local --strip-components=1 \
  && rm "phantomjs-$PHANTOSJS_VERSION-linux-x86_64.tar.bz2" \
  && ln -s /usr/local/phantomjs /usr/bin/phatomjs

# install maven
RUN mkdir -p /usr/local/maven /usr/local/maven/ref \
  && curl -SLO http://apache.osuosl.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
  && tar -xf "apache-maven-$MAVEN_VERSION-bin.tar.gz" -C /usr/local --strip-components=1 \
  && rm "apache-maven-$MAVEN_VERSION-bin.tar.gz" \
  && ln -s /usr/local/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME /usr/local/maven

# make /tmp available to all users.
RUN chmod 777 -R /tmp && chmod o+t -R /tmp

VOLUME /workspace
WORKDIR /workspace

ENTRYPOINT [ "gulp" ]