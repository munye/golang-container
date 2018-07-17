FROM golang:latest

ENV NAME=golang \ 
    VERSION=1.9 

ENV SUMMARY="Platform for building and running Go $VERSION microservices" \
    DESCRIPTION="Platform for building and running Go $VERSION microservices,\
                 managed with gin-gonic/gin and exposing metrics via gin-gomonitor"

LABEL summary="$SUMMARY" \ 
      description="$DESCRIPTION" \
      io.k8s.description="$DESCRIPTION" \
      io.k8s.display-name="Go $VERSION" \
      io.openshift.tags="builder,microservices,coda-hale,metrics,go,golang, \
                        golang19, gin,gin-gonic" \ 
      name="golang" \ 
      version="$VERSION" \ 
      maintainer="Munye <ebergonzi@afip.gob.ar>"

EXPOSE 8080

RUN go get github.com/gin-gonic/gin && \ 
    go get github.com/szuecs/gin-gomonitor && \ 
    go get github.com/szuecs/gin-gomonitor/aspects && \ 
    go get gopkg.in/mcuadros/go-monitor.v1/aspects

COPY ./s2i/bin/ /sti_scripts

COPY ./root/ /

RUN useradd -U -u 1001 openshift

RUN chown -R 1001:1001 /sti_scripts

USER 1001

CMD /sti_scripts/usage
