# Microservices Project

This repository contains a Docker Compose setup for running a microservices architecture with Krakend, Grafana, Prometheus, and Jaeger.

## Requirements

- Docker
- Docker Compose

## Services

- **Krakend EE**: API Gateway 
- **Grafana**: Data visualization and monitoring 
- **Prometheus**: Monitoring and alerting 
- **Jaeger**: Distributed tracing 

## Setup

### Clone the Repository

```sh
git clone https://github.com/Kavindu-Jayasinghe/krakend-micro.git
cd krakend-with-grafana-prometheus-and-jaeger-microservices
```
# Start the Services
## To start all the services, run:
```
docker-compose up -d
```
# Stop the Services
## To stop all the services, run:
```
docker-compose down

```
# Configuration
## Krakend 
The Krakend configuration is defined in ./config/krakend/krakend.json. You can modify this file to change the API gateway behavior(dosn't have a UI).
```localhost:8080```
## Grafana 
Grafana is configured to use Prometheus as a data source and includes dashboards for monitoring. Configuration files are located in ./config/telemetry-dashboards/grafana/.
```localhost:4000```
## Prometheus 
Prometheus is configured to scrape metrics from various services. The configuration file is located at ./config/telemetry-dashboards/prometheus/prometheus.yml.
```localhost:9090```
## Jaeger 
from Jaeger update there is a problem with pushing span data to jaeger if you face some error like this, 
```
▶ ERROR [SERVICE: OpenTelemetry] traces export: context deadline exceeded: rpc error: code = Unavailable desc = connection error: desc = "transport: Error while dialing: dial tcp localhost:4317: connect: connection refused"
```
it becouse, when running in container environment the endpoints are likely unreachable from other containers the fix will be available in the next release. Meanwhile, the workaround is to instruct Jaeger to listen on 0.0.0.0, as in this fix:
```
 - COLLECTOR_OTLP_GRPC_HOST_PORT=0.0.0.0:4317
 - COLLECTOR_OTLP_HTTP_HOST_PORT=0.0.0.0:4318
```
Jaeger is set up to collect and visualize traces. No additional configuration is required.
```localhost:16686```
## API Endpoints
Krakend API
Endpoint: /product
Method: 'GET'
Description: Retrieves product information from the backend service.
Or you can add endpoints as your need in krakend.json, /product is basic sample endpoint. use krakend [designer](https://designer.krakend.io/#!/) for define endpoints you can find information in [documentation](https://www.krakend.io/docs/)
## Example Request
```
curl -X GET http://localhost:8080/product

```
## or postman
method "GET"
```
http://localhost:8080/__health
http://localhost:8080/product
```
## Logs
## Logs for each service can be viewed using the following commands:
 Krakend
 ```
docker-compose logs krakend_ee

```
Grafana
```
docker-compose logs grafana

```
Prometheus
```
docker-compose logs prometheus

```
Jaeger
```
docker-compose logs jaeger

```
## or 
## if you use docker desktop you can find logs, 
docker desktop -> containers -> krakend-with-grafana-prometheus-and-jaeger-microservices
 -> container name -> logs 
# Ports
Krakend EE: '1234','8080'

Grafana: '4000'

Prometheus: '9090'

Jaeger: '16686','14268','64317','64318'

# Notes
## The krakend/krakend-ee:2.6-watch image is used for development purposes. Do not use this image in production.
## Default Grafana admin credentials are 'admin'/'123'.
## API Endpoints that genarated using Ai like chatGPT can be return 404 in this case you have to define endpoints your self.


