# Agency Observability

A ready-to-go observability system for monitoring and tracing applications. This repository provides a pre-configured setup for Grafana, Loki, Tempo, and OpenTelemetry Collector to enable logs, metrics, and traces collection.

## Overview

This system is designed to simplify the setup of an observability stack for development and production environments. It includes:

- **Grafana**: For visualization and dashboards.
- **Loki**: For log aggregation and storage.
- **Tempo**: For distributed tracing.
- **OpenTelemetry Collector**: For collecting, processing, and exporting telemetry data.

## Prerequisites

- Docker
- Docker Compose

## Setup Instructions

1. Clone this repository:

   ```bash
   git clone <repository-url>
   cd agency-observability
   ```

2. Configure the environment:

   - Update the `GF_SECURITY_ADMIN_PASSWORD` in the `docker-compose.yml` file to set a secure password for Grafana.

3. Start the services:

   ```bash
   docker-compose up -d
   ```

4. Access the services:

   - **Grafana**: Open your browser and navigate to `http://localhost:3012`. Use `admin` as the username and the password you set in the `docker-compose.yml` file.
   - **Loki**: Accessible via Grafana for logs.
   - **Tempo**: Accessible via Grafana for traces.

## Configuration

### Grafana

Grafana is configured to expose port `3012` on your host machine. You can customize the port and other settings in the `docker-compose.yml` file.

### OpenTelemetry Collector

The OpenTelemetry Collector is configured to receive telemetry data on ports `4317` (gRPC) and `4318` (HTTP). It processes and exports logs to Loki and traces to Tempo. The configuration is defined in `otel-config.yaml`.

### Loki

Loki is configured to store logs and is accessible via the OpenTelemetry Collector. No additional configuration is required unless you want to customize storage or retention policies.

### Tempo

Tempo is configured to store traces locally and is accessible via the OpenTelemetry Collector. The configuration is defined in `tempo-config.yaml`.

## Usage

### Sending Telemetry Data

To send telemetry data to this observability system, configure your applications to export logs and traces to the OpenTelemetry Collector:

- **Logs**: Send logs to `http://<your-host>:4318/v1/logs`.
- **Traces**: Send traces to `http://<your-host>:4317/v1/traces`.

### Viewing Data in Grafana

1. Open Grafana in your browser.
2. Navigate to the "Explore" section.
3. Select the appropriate data source (Loki for logs, Tempo for traces).
4. Query and visualize your telemetry data.

## Customization

- **Grafana Dashboards**: Import custom dashboards or configure existing ones to suit your needs.
- **Retention Policies**: Adjust the retention policies in `tempo-config.yaml` to control how long traces are stored.
- **Batch Processing**: Modify the batch processor settings in `otel-config.yaml` to optimize performance.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.