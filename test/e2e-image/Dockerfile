FROM quay.io/kubernetes-ingress-controller/e2e:v05062019-b4f2880ee AS BASE

FROM quay.io/kubernetes-ingress-controller/debian-base-amd64:0.1

RUN clean-install \
    ca-certificates \
    bash \
    curl \
    tzdata

RUN curl -Lo /usr/local/bin/kubectl \
    https://storage.googleapis.com/kubernetes-release/release/v1.14.1/bin/linux/amd64/kubectl \
    && chmod +x /usr/local/bin/kubectl

COPY --from=BASE /go/bin/ginkgo /usr/local/bin/

COPY e2e.sh             /e2e.sh
COPY manifests          /manifests
COPY wait-for-nginx.sh  /
COPY e2e.test           /

CMD [ "/e2e.sh" ]
