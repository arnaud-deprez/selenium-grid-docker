FROM selenium/node-firefox:3.14.0

ENV HOME=/home/seluser

USER root

COPY ./contrib /usr/local/bin

RUN chown -R 1001:0 /opt/selenium && \
  /usr/local/bin/fix-permissions /opt/selenium && \
  /usr/local/bin/fix-permissions /var/log &&\
  /usr/local/bin/fix-permissions /var/run &&\
  /usr/local/bin/fix-permissions $HOME

USER 1001
WORKDIR $HOME
