# Copyright The OpenTelemetry Authors
# SPDX-License-Identifier: Apache-2.0


FROM --platform=${BUILDPLATFORM} eclipse-temurin:21-jdk AS builder

WORKDIR /usr/src/app

COPY gradlew* settings*.gradle ./   build.gradle* ./
COPY gradle ./

RUN chmod +x ./gradlew
RUN ./gradlew
RUN ./gradlew downloadRepositories

COPY . .

RUN chmod +x ./gradlew
COPY ./pb ./proto

RUN chmod +x ./gradlew
RUN ./gradlew installDist -PprotoSourceDir=./proto

FROM eclipse-temurin:21-jre
WORKDIR /usr/src/app

COPY --from=builder /usr/src/app ./

ENV AD_PORT=8080

ENV FEATURE_FLAG_GRPC_SERVICE_ADDR=featureflagservice:50053

ENTRYPOINT [ "build/install/opentelemetry-demo-ad/bin/./Ad" ]

