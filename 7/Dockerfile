FROM centos/s2i-base-centos7

ENV LLVM_VERSION="5.0.x" \
    SUMMARY="Platform for building projects with clang/llvm" \
    DESCRIPTION="$SUMMARY"


LABEL summary="$SUMMARY" \
      description="$DESCRIPTION" \
      io.k8s.description="$DESCRIPTION" \
      io.k8s.display-name="$LLVM_VERSION" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,llvm,clang" \
      com.redhat.component="llvm-toolset-7-docker" \
      name="centos/llvm-toolset-7-centos7" \
      version="5.0.1" \
      maintainer="SoftwareCollections.org <sclorg@redhat.com>"

RUN yum install -y centos-release-scl-rh && \
    yum-config-manager --enable centos-sclo-rh-testing && \
    INSTALL_PKGS="llvm-toolset-7 llvm-toolset-7-cmake" && \
    yum install -y --setopt=tsflags=nodocs $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y

COPY ./root /
COPY ./s2i/bin/ $STI_SCRIPTS_PATH

# Drop the root user and make the content of /opt/app-root owned by user 1001
RUN chown -R 1001:0 /opt/app-root && \
    chmod -R ug+rwx /opt/app-root && \
    rpm-file-permissions

# Enable the SCL for all bash scripts.
ENV BASH_ENV=/opt/app-root/etc/scl_enable \
    ENV=/opt/app-root/etc/scl_enable \
    PROMPT_COMMAND=". /opt/app-root/etc/scl_enable" \
    CC="clang" \
    CXX="clang++"

USER 1001

CMD $STI_SCRIPTS_PATH/usage
