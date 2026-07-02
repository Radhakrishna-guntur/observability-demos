# Observability-demos
Welcome to Observability Stuff. This repository contains the code and detailed explanations for setting up and understanding observability in Kubernetes using Prometheus, Grafana, Elasticsearch Fluentbit, Kibana, Jaeger, groundcover(eBPF), opentelemetry e.t.c.,.

**What is Graphana Loki**

Loki is a highly efficient log aggregation system designed to store and query logs from your applications and infrastructure. Unlike traditional solutions such as Elasticsearch, which index the entire log content, Loki focuses solely on indexing metadata tags (labels) that accompany the logs. This unique approach significantly reduces costs and simplifies operational management.

When issues arise, you can quickly diagnose problems by querying Loki for logs within a specific timeframe. Its cost-effective design and simplicity make Loki an attractive alternative for organizations looking to avoid the complexities and overhead associated with more intricate logging solutions.

For instance, managing Elasticsearch can often require hiring dedicated personnel because of its configuration and maintenance challenges. In contrast, Loki’s straightforward design means you can achieve high performance and cost efficiency by indexing only the essential label data rather than the full log text.

**Log Collection and Ingestion**

Loki is known for its flexibility in log collection. Although Loki provides its own log collection client, Promtail, you are not limited to it. Other popular log shippers such as Fluentd and Logstash can also be used in your environment. After installing the chosen agent on your servers, these agents continuously collect logs and stream the data to the Loki server.

**Log Processing and Labeling**

Once logs are received by the Loki server, the system parses the logs to extract the fundamental log content and its associated metadata, known as labels. These labels are configured by you and are essential for Loki's performance, as only these labels are indexed rather than the entire log message. This design choice reduces indexing overhead and streamlines log queries.

**Scalable and Cost-Efficient Storage**

Loki supports multiple storage backends for the log data. You can choose from traditional local file systems or leverage modern object storage solutions such as Amazon S3. Object storage is particularly beneficial as it often reduces operational costs while providing high scalability and ease of management.

**Querying Logs with LogQL**

For retrieving and analyzing logs, Loki uses its powerful query language called LogQL. With LogQL, you can filter logs, narrow down searches by timeframe, and perform various analytical queries. Due to Loki’s integration within the Grafana ecosystem, many users prefer querying logs via Grafana’s intuitive graphical interface, although a command-line interface (CLI) is also available for direct queries.

After successfully configured Promtail on multiple nodes to collect log files from both system directories and your application directory. This setup makes monitoring and troubleshooting your API logs through Grafana an efficient.


**Loki in Kubernetes**

We'll explore how to collect logs from applications running on a Kubernetes cluster using Loki, Promtail, and Grafana. This guide focuses on an in-cluster deployment, making it easier to manage your logging stack as part of your existing Kubernetes environment.

When running multiple containers on different cluster nodes, collecting logs from specific containers and applications reliably becomes crucial. One common strategy is to deploy a Loki instance directly on your Kubernetes cluster. Although Loki and Grafana can be deployed externally, hosting them within the cluster simplifies management and integration.


**How It Works**

Each node in your Kubernetes cluster runs a kubelet process that collects log data from its pods. To forward these logs to the Loki instance, you'll deploy Promtail on each node. Promtail gathers logs from all pods and routes them to Loki. Kubernetes ensures that a Promtail container is automatically deployed on every node through the use of daemon sets. When new nodes join the cluster, Kubernetes deploys Promtail on these as well.


**Simplifying Deployment with Helm**

Manually deploying Loki, Promtail, and Grafana can be quite time-consuming due to complex configurations. Thankfully, Helm charts are available for these tools. With just a few commands, Helm can deploy and configure Loki, Grafana, and Promtail, dramatically reducing the manual setup effort.

**Step-by-Step Process**

Follow these steps to set up your logging stack on Kubernetes:

**Deploy Loki:** Set up a Loki instance on your Kubernetes cluster.

**Deploy Grafana: **Configure a Grafana dashboard for visualization, whether it is hosted within Kubernetes or externally.
**Deploy Promtail: **Use a daemon set to deploy Promtail on every node so it can collect logs from all pods.
**Use Helm:** Leverage a Helm chart to automate the configuration of Loki, Grafana, and Promtail.

By following these steps and utilizing a Helm chart, you can set up effective log collection and visualization in your Kubernetes environment with minimal manual configuration.

**Key Takeaway**

Leveraging the combination of Helm charts with Loki, Grafana, and Promtail significantly enhances your logging infrastructure, making it easier to monitor, analyze, and debug your applications.

**Conclusion**

This article on deploying Loki, Grafana, and Promtail within a Kubernetes cluster using a Helm chart. Throughout the lesson, we demonstrated how to efficiently collect application logs and customize log processing so that key information is extracted and labeled. 

This log enrichment enables Loki to index and filter logs more effectively, providing better observability and troubleshooting capabilities in your Kubernetes environment.



