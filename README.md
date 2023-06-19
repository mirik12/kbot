Deployment of Monitoring Stack in Kubernetes
This step-by-step guide will help you deploy a monitoring stack that includes OpenTelemetry, Prometheus, Fluentbit, Grafana Loki, and Grafana in Kubernetes.

Prerequisites
Kubernetes installed.
Helm installed.
Flux installed.
Steps
Install Flux in your cluster:

bash
Copy code
flux install
Open your Flux repository in a browser, open the .flux.yaml file, and set git.path to the path of your project.

Change git.url in .flux.yaml file to the URL of your Git repository.

Run the command:

bash
Copy code
flux reconcile source git flux-system
Run the command:

bash
Copy code
kubectl apply -f <path-to-your-loki-config> # Example: kubectl apply -f /path/to/loki-local-config.yaml
Install and configure OpenTelemetry and Fluentbit:

Add the OpenTelemetry repository:

bash
Copy code
helm repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts
helm repo update
Deploy OpenTelemetry Collector:

bash
Copy code
helm upgrade --install otel-collector open-telemetry/opentelemetry-collector -n <your-namespace> --create-namespace
Add the Fluentbit repository:

bash
Copy code
helm repo add fluent https://fluent.github.io/helm-charts
helm repo update
Deploy Fluent Bit:

bash
Copy code
helm upgrade --install fluent-bit fluent/fluent-bit -n <your-namespace>
To set up Prometheus, run the following commands:

bash
Copy code
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm upgrade --install prometheus prometheus-community/prometheus -n <your-namespace> --create-namespace
To set up Grafana Loki, run the following commands:

bash
Copy code
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
helm upgrade --install loki grafana/loki -n <your-namespace>
To set up Grafana, run the following commands:

bash
Copy code
helm upgrade --install grafana grafana/grafana -n <your-namespace>
By following these steps, you'll deploy all necessary monitoring components in your Kubernetes cluster.

![Prometheus Create](/Users/mark/Downloads/rest/dev/kbot-3/images/prometheuscreate.png)
![Prometheus Graph](/Users/mark/Downloads/rest/dev/kbot-3/images/prometheusgraph.png)
![Loki Create](/Users/mark/Downloads/rest/dev/kbot-3/images/lokicreate.png)
![Query Inspector](/Users/mark/Downloads/rest/dev/kbot-3/images/queryinspector.png)

