ARG version=tip
FROM registry.access.redhat.com/ubi8/ubi-minimal:8.4

ARG cnb_uid=1000
ARG cnb_gid=1001

LABEL io.buildpacks.stack.id=openshift.serverless.functions.nodejs

ENV CNB_STACK_ID=openshift.serverless.functions.nodejs
ENV CNB_USER_ID=${cnb_uid}
ENV CNB_GROUP_ID=${cnb_gid}
ENV NODE_PATH $HOME/node_modules
ENV NODE_ENV production
ENV PORT 8080
ENV HOME /workspace

USER root
COPY ./nodejs.module /etc/dnf/modules.d
RUN microdnf install --nodocs -y shadow-utils tar nodejs && \
  groupadd -g ${cnb_gid} cnb && \
  useradd -u ${cnb_uid} -g cnb -s /bin/bash cnb && \
  mkdir ${HOME} && \
  chown cnb:cnb ${HOME}

USER ${cnb_uid}:${cnb_gid}
WORKDIR ${HOME}
