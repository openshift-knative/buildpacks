ARG version=tip
FROM registry.access.redhat.com/ubi8/ubi:8.4

ARG cnb_uid=1000
ARG cnb_gid=1001

LABEL io.buildpacks.stack.id=openshift.serverless.functions.nodejs

ENV CNB_STACK_ID=openshift.serverless.functions.nodejs
ENV CNB_USER_ID=${cnb_uid}
ENV CNB_GROUP_ID=${cnb_gid}
ENV HOME /workspace

USER root
COPY ./nodejs.module /etc/dnf/modules.d
RUN dnf install --nodocs -y nodejs tar git && \
  groupadd -g ${cnb_gid} cnb && \
  useradd -u ${cnb_uid} -g cnb -s /bin/bash cnb && \
  mkdir ${HOME} && \
  chown ${cnb_uid}:${cnb_gid} ${HOME}

WORKDIR ${HOME}
USER ${cnb_uid}:${cnb_gid}
