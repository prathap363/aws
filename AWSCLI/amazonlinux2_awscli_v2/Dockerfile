# Based upon https://github.com/aws/aws-cli/blob/2.0.10/docker/Dockerfile
FROM amazonlinux:2 as installer
ARG TERRAFORM_VERSION
RUN yum update -y \
  && yum install -y unzip \
  && yum install -y tar \
  && yum install -y wget \
  yum -y install gzip.x86_64 \
  && curl https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip -o awscli-exe-linux-x86_64.zip \
  && unzip -q awscli-exe-linux-x86_64.zip \
  # The --bin-dir is specified so that we can copy the
  # entire bin directory from the installer stage into
  # into /usr/local/bin of the final stage without
  # accidentally copying over any other executables that
  # may be present in /usr/local/bin of the installer stage.
  && ./aws/install --bin-dir /aws-cli-bin/ \
  && curl "https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip" -o terraform.zip \
  && unzip terraform.zip \
  && wget -q "https://dl.k8s.io/release/v1.27.2/bin/linux/amd64/kubectl"\
  && wget -q "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz" \
 && tar -xf eksctl_Linux_amd64.tar.gz

FROM amazonlinux:2
COPY --from=installer /usr/local/aws-cli/ /usr/local/aws-cli/
COPY --from=installer /aws-cli-bin/ /usr/local/bin/
COPY --from=installer terraform /usr/bin/
COPY --from=installer kubectl /usr/local/bin/
COPY --from=installer eksctl /usr/local/bin/


RUN yum update -y \
  && yum install -y less groff jq \
  && yum clean all

RUN chmod 755 /usr/local/bin/kubectl 

ENTRYPOINT ["/bin/sh"]