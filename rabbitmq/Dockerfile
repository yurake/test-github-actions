FROM rabbitmq:3.9.7-management-alpine
ARG BUILD_DATE
ARG VCS_REF
# renovate: datasource=repology depName=alpine_3_12/tzdata
ENV TZDATA_VERSION="2021a-r0"
LABEL org.label-schema.build-date=$BUILD_DATE org.label-schema.vcs-ref=$VCS_REF \
    org.label-schema.vcs-url="https://github.com/yurake/k8s-3tier-webapp"
RUN apk update && \
    apk --no-cache add tzdata=${TZDATA_VERSION} && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    apk del tzdata
COPY custom_definitions.json /etc/rabbitmq/
RUN printf 'management.load_definitions = /etc/rabbitmq/custom_definitions.json\n' >> /etc/rabbitmq/rabbitmq.conf
RUN rabbitmq-plugins enable rabbitmq_prometheus
