What is Datadog?

Datadog is a cloud-based observability and security platform that provides monitoring, alerting, and analytics for applications, infrastructure, containers, databases, and cloud services.

It brings together logs, metrics, and traces into a single platform → this is called observability.

Datadog is SaaS-based (Software as a Service), meaning most heavy lifting (data storage, visualization, analytics) happens in the Datadog cloud, while lightweight agents collect data from your systems.

👉 Simple view: Install Datadog Agent → it collects system + app data → sends to Datadog backend → you use dashboards, alerts, reports.

🔹 Why Datadog?

End-to-End Visibility: Infrastructure, databases, applications, containers, logs, and security, all in one place.

Wide Monitoring Coverage:

Infrastructure monitoring

Database monitoring

Cloud service monitoring

Application Performance Monitoring (APM)

Real User Monitoring (RUM)

Security monitoring

Synthetic monitoring (simulate user behavior)

Dashboards & Alerts: Comes with pre-built dashboards, and you can create custom monitors/alerts.

Integrations: 500+ integrations (AWS, Azure, GCP, Kubernetes, Docker, etc.).

🔹 Datadog Architecture (Step-by-Step)
 Application/Host --> Datadog Agent --> Datadog Backend (Cloud) --> User

🟢 Components

Host (Server, VM, Container)

Your application runs here (Python, Java, Node, etc.).

Datadog Agent is installed on the host.

Datadog Agent

Main process installed on each host.

Collects metrics, traces, and logs.

Contains multiple subcomponents:

Collector → gathers system metrics (CPU, memory, disk).

DogStatsD → receives custom app metrics via UDP.

Forwarder → batches, compresses, and sends data to Datadog Cloud.

Buffer → temporary storage if network is down.

APM Agent (Optional)

Collects application traces (slow queries, bottlenecks).

Process Agent (Optional)

Collects live process info from hosts/containers.

UI Agent (Optional)

Provides a local UI to see Datadog Agent status/config.

Datadog Backend (Cloud)

Centralized SaaS platform (https://app.datadoghq.com
).

Stores and analyzes logs/metrics/traces.

Provides dashboards, alerts, ML-based anomaly detection.

User

Interacts with dashboards, creates alerts, queries logs.

🔹 Datadog Configuration

Main config file:
/etc/datadog-agent/datadog.yaml

Integration configs:
/etc/datadog-agent/conf.d/

Example config snippet:
tags:
  - "os:ubuntu"
  - "env:production"
  - "team:devops"

🔹 Tagging in Datadog

Tags = labels (key:value) that help organize, filter, and search telemetry.

Examples:

env:prod, env:dev

region:us-east-1

service:payments

👉 Use tags in dashboards, alerts, and log queries.

🔹 Live Process Monitoring

Datadog can show all processes running on your hosts/containers.

Useful to track CPU/memory usage per process, detect rogue apps.

Enable in /etc/datadog-agent/system-probe.yaml:

process_config:
  process_collection:
    enabled: true


Restart Agent:

sudo systemctl restart datadog-agent.service

🔹 Scrubbing Sensitive Data

Sometimes process command lines or logs contain secrets (passwords, API keys).

By default, Datadog scrubs known sensitive fields.

You can add your own custom sensitive words:

process_config:
  process_collection:
    enabled: true
    scrub_args: true
    custom_sensitive_words: ['password', 'token', 'user']

🔹 Running Datadog in Docker / Kubernetes

Instead of installing on each VM, you can run Datadog Agent as a container:

docker run -d --name dd-agent \
  -e DD_API_KEY=<YOUR_API_KEY> \
  -e DD_SITE=datadoghq.com \
  -v /var/run/docker.sock:/var/run/docker.sock:ro \
  -v /proc/:/host/proc/:ro \
  -v /sys/fs/cgroup/:/host/sys/fs/cgroup:ro \
  gcr.io/datadoghq/agent:7


👉 This is especially useful in Kubernetes clusters → one agent per node.

🔹 Metric Types in Datadog

Count

Number of events in a time interval.

Example: # of HTTP requests.

Rate

Events per second (Count ÷ Time).

Example: Requests/sec.

Gauge

Last reported value in interval.

Example: CPU usage, memory usage, temperature.

Set

Counts unique values.

Example: unique users.

Histogram

Distribution of values over an interval.

Example: response time (p50, p95, p99).

👉 Agent flushes every 10 seconds, so values are aggregated in that window.

🔹 Key Features of Datadog

Dashboards → Pre-built & custom.

Alerts/Monitors → Thresholds, anomaly detection, forecasting.

Log Management → Ingest, filter, search, and analyze logs.

APM (Traces) → Detect bottlenecks in distributed applications.

RUM (Real User Monitoring) → See frontend (browser/mobile) user experience.

Synthetic Monitoring → Simulate user requests (API tests, uptime checks).

Security Monitoring → Detect suspicious behavior, intrusion attempts.

Integrations → AWS, Azure, GCP, Kubernetes, Docker, PostgreSQL, Nginx, etc.

🔹 Practical Workflow Example

Install Datadog Agent on VM/container.

Configure tags (env, service, team).

Agent collects:

Host metrics (CPU, memory, disk).

Logs from apps.

Traces from requests.

Agent sends data to Datadog backend (HTTPS).

User creates dashboards/alerts:

Example: "Alert if CPU > 90% for 5 minutes."

Datadog notifies via email/Slack/PagerDuty.

✅ In summary:
Datadog is not just a monitoring tool; it’s a full-stack observability platform. It unifies metrics, logs, traces, security, and user experience monitoring in one place, making it extremely popular in DevOps, SRE, and Cloud-native environments.
