FROM docker.io/fedora:33

ENV SUMMARY="Image based on fedora which allows using of source-to-image." \
  DESCRIPTION="The s2i-base image provides all the tools needed to use source-to-image functionality while keeping the image size as small as possible"

LABEL io.k8s.description="$DESCRIPTION" \
  io.k8s.display-name="s2i base fedora 33" \
  io.openshift.s2i.scripts-url=image:///usr/libexec/s2i \
  io.s2i.scripts-url=image:///usr/libexec/s2i \
  name="alexanderniebuhr/s2i-base-fedora33" \
  version="1.0.0" \
  maintainer="Alexander Niebuhr <45965090+alexanderniebuhr@users.noreply.github.com>"

ENV APP_ROOT=/opt/app-root \
  HOME=/opt/app-root/src \
  PATH=/opt/app-root/src/bin:/opt/app-root/bin:$PATH \
  PLATFORM="fedora"

RUN mkdir -p ${HOME}/.pki/nssdb && chown -R 1001:0 ${HOME}/.pki && yum install -y bsdtar findutils gettext  glibc-langpack-en groff-base rsync tar unzip \
  rpm -V bsdtar findutils gettext  glibc-langpack-en groff-base rsync tar unzip && yum clean all -y

COPY ./libs/ /

WORKDIR ${HOME}

ENTRYPOINT ["container-entrypoint"]
CMD ["base-usage"]

# Reset permissions of modified directories and add default user
RUN rpm-file-permissions && \
  useradd -u 1001 -r -g 0 -d ${HOME} -s /sbin/nologin \
  -c "Default Application User" default && \
  chown -R 1001:0 ${APP_ROOT}