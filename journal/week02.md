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

### Detailed understanding of AWS XRay traces
This was implemented by intalling XRAY Daemon onto the Docker compose. 

#### Installing the Honeycomb.io datasets for capturing the traces onto the platform 

#### Instalation of Rollbar - Issues faced
Many issues were faced when installing Rollbar. Having searched on many Github repo, The code provided on the bootcamp nothing was working. 
This was fixed using the following code for connecting Rollbar to Flask: 
```
def init_rollbar():
    """init rollbar module"""
    rollbar.init(
        # access token for the demo app: https://rollbar.com/demo
        'access to rollbar ID inserted here',
        # environment name
        'flasktest',
        # server root directory, makes tracebacks prettier
        root=os.path.dirname(os.path.realpath(__file__)),
        # flask already sets up logging
        allow_logging_basic_config=False)

    # send exceptions from `app` to rollbar, using flask's signal system.
    got_request_exception.connect(rollbar.contrib.flask.report_exception, app)
```
