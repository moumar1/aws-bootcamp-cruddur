# Week 2 — Distributed Tracing

Starting off by setting the enviroment variables from Honeycomb.io 
```
OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
OTEL_SERVICE_NAME: "backend-flask"
```
#### OTEL TELEMETRY is part of the CNCF Cloud native compute foundation which runs Kubernetes. An open standard for cross platform. 

Add following lines into requirements.txt

```
opentelemetry-api 
opentelemetry-sdk 
opentelemetry-exporter-otlp-proto-http 
opentelemetry-instrumentation-flask 
opentelemetry-instrumentation-requests
```
enter the following in Terminal ``` pip install -r requirements.txt ```
