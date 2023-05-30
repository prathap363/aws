FROM alpine:latest
RUN apk --no-cache add python3 py3-pip

#Installing AWSCLI  
RUN  pip3 install --upgrade pip \
  && pip3 install --no-cache-dir awscli \
  && apk add mandoc man-pages


#Installing EKSCTL    
RUN wget "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz" && tar -xzf eksctl_Linux_amd64.tar.gz -C /usr/local/bin && rm eksctl_Linux_amd64.tar.gz
CMD ["sh"]
