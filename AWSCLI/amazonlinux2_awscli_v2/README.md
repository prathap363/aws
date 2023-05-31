This docker file has below componentes installed and pre-configured

1.python3
2.EKSCTL latest
3.kubectl V1.27.2
4.awscli v2
5.terraform v [custom - needs to be specified while building the image ]

step to build image
docker image build -t <imagename> --build-arg TERRAFORM_VERSION=1.4.6 .