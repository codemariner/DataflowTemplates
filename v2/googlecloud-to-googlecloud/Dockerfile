FROM gcr.io/dataflow-templates-base/java17-template-launcher-base:latest AS template_launcher
FROM docker.artifactory.banno-tools.com/java:17

COPY --from=template_launcher /opt/google/dataflow/java_template_launcher /opt/google/dataflow/java_template_launcher

ARG VERSION
ARG ENV_NAME
ARG PIPELINE
ARG TABLE
ARG FAILURE_TABLE

ARG WORKDIR=/dataflow/template/target
RUN mkdir -p ${WORKDIR}
WORKDIR ${WORKDIR}

COPY target/googlecloud-to-googlecloud-1.0-SNAPSHOT.jar ${WORKDIR}
ENV FLEX_TEMPLATE_JAVA_CLASSPATH="${WORKDIR}/googlecloud-to-googlecloud-1.0-SNAPSHOT.jar"
ENV FLEX_TEMPLATE_JAVA_MAIN_CLASS="com.google.cloud.teleport.v2.templates.spannerchangestreamstobigquery.SpannerChangeStreamsToBigQuery"

ENV VERSION=$VERSION
ENV ENV_NAME=$ENV_NAME
ENV PIPELINE=$PIPELINE
ENV TABLE=$TABLE
ENV FAILURE_TABLE=$FAILURE_TABLE

ENTRYPOINT ["/opt/google/dataflow/java_template_launcher"]
