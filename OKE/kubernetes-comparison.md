---
title: "Kubernetes: A comparison of managed engines"
description: An extensive comparison of the four most prolific managed Kubernetes offerings.
author:
  name: Eli Schilling
  bio: Oracle DevRel Advocate, cloud native app dev and DevOps.
  github: "https://github.com/oracle-devrel"
  youtube: "https://www.youtube.com/c/oracledevs/playlists"
  email: eli.schilling@oracle.com
parent: [tutorials]
categories: [cloudapps, clouddev, modernize, enterprise]
date: 2023-01-23 08:00
modified: 2023-01-31 08:00

---

## **General Information**

This document contains an extensive, though not exhaustive comparison of the four most prolific managed Kubernetes offerings: Oracle Container Engine for Kubernetes (OKE), Amazon Elastic Kubernetes Service (EKS), Azure Kubernetes Service (AKS), and Google Kubernetes Engine (GKE). The comparison was developed with input from the community and will continue to be revised as the technology changes.

First published January 7th, 2023, this document will be updated regularly to ensure consistent and relevant information is made available. Should you have any questions or wish to contribute feedback, you may [reach us any time on Slack!]

Quick reference

- [Currently supported Kubernetes version(s)]
- [\# of supported minor version releases]
- [Original GA release date]
- [Pricing]
- [CNCF Kubernetes Conformance]
- [CLI support]
- [Control-plane upgrade process]
- [Node upgrade process]
- [Node OS]
- [Container runtime]
- [Control plane high availability options]
- [Control plane SLA]
- [Uptimes SLA]
- [SLA financially-backed]
- [GPU support]
- [Container performance metrics]
- [Monitoring]
- [Node health monitoring]
- [Autoscaling]
- [Serverless computing]
- [Accessibility]
- [Bare metal clusters]
- [Worker node types]
- [Tools for developers]

<table>
<colgroup>
<col style="width: 15%" />
<col style="width: 23%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th><strong>OKE</strong></th>
<th>EKS</th>
<th>AKS</th>
<th>GKE</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="GI_CurrentKs8Version" class="anchor"></span>Currently supported Kubernetes version(s)</td>
<td><p>1.25.4, 1.24.1, 1.23.4, 1.22.5</p>
<p>(<a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengaboutk8sversions.htm">source</a>)</p></td>
<td><p>1.24.7, 1.23.13, 1.22.15, 1.21.14</p>
<p>(<a href="https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-versions.html">source</a>)</p></td>
<td><p>1.24.6, 1.23.12, 1.22.15</p>
<p>Current minor version and previous 2 minor versions (<a href="https://docs.microsoft.com/en-us/azure/aks/supported-kubernetes-versions?tabs=azure-cli">source</a>)</p></td>
<td><p>1.24.1, 1.23.4, 1.22.5, 1.21.5</p>
<p>(rolling support for the most current versions of K8s; <a href="https://cloud.google.com/kubernetes-engine/versioning">source</a>)</p></td>
</tr>
<tr class="even">
<td><span id="GI_SupportedMinorVersions" class="anchor"></span># of supported minor version releases</td>
<td><a href="https://docs.oracle.com/en-us/iaas/releasenotes/changes/82948243-0363-414d-ad28-72a7653a4f24/">3</a></td>
<td>&gt;=3 + 1 deprecated</td>
<td>3</td>
<td>4</td>
</tr>
<tr class="odd">
<td><span id="GI_ReleaseDate" class="anchor"></span>Original GA release date</td>
<td>May 2018</td>
<td>June 2018</td>
<td>June 2018</td>
<td>August 2015</td>
</tr>
<tr class="even">
<td><span id="GI_Pricing" class="anchor"></span>Pricing</td>
<td>All management costs are <a href="https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm">free</a></td>
<td><a href="https://aws.amazon.com/eks/pricing/"><u>$0.10/hour (USD)</u></a> per cluster + standard costs of EC2 instances and other resources</td>
<td><a href="https://azure.microsoft.com/en-ca/pricing/details/kubernetes-service/"><u>Pay-as-you-go</u></a>: Standard costs of node VMs and other resources</td>
<td><a href="https://cloud.google.com/kubernetes-engine/pricing"><u>$0.10/hour (USD)</u></a> per cluster + standard costs of GCE machines and other resources</td>
</tr>
<tr class="odd">
<td><a href="https://www.cncf.io/certification/software-conformance/">CNCF Kubernetes Conformance</a></td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengoverview.htm">Yes</a> (also, <a href="https://www.cncf.io/certification/software-conformance/">here</a>)</td>
<td>Yes</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><span id="GI_CNCFcertifiedVersion" class="anchor"></span>CLI support</td>
<td>Full support of Kubernetes clusters;<br />
<strong><a href="https://docs.oracle.com/en-us/iaas/Content/API/Concepts/devcloudshellintro.htm">Oracle Cloud Shell</a>;</strong> <a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengaccessingclusterkubectl.htm">Kubectl</a> support</td>
<td>Full support of Kubernetes clusters; Kubectl support</td>
<td>Full support of Kubernetes clusters; Kubectl support</td>
<td>Full support of Kubernetes clusters; Kubectl support</td>
</tr>
<tr class="odd">
<td><span id="GI_ControlPlaneUpgradeProcess" class="anchor"></span>Control-plane upgrade process</td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengupgradingk8smasternode.htm">User-initiated</a> All system components update with cluster upgrade</td>
<td><a href="https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html"><u>User initiated</u></a>; User must also manually update the system services that run on nodes (e.g., kube-proxy, coredns, AWS VPC CNI)</td>
<td><p><a href="https://docs.microsoft.com/en-us/azure/aks/upgrade-cluster"><u>User initiated</u></a></p>
<p>All system components update with cluster upgrade</p></td>
<td><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/cluster-upgrades"><u>Automatically upgraded</u></a> by default; <a href="https://cloud.google.com/kubernetes-engine/docs/how-to/upgrading-a-cluster"><u>can be user-initiated</u></a></td>
</tr>
<tr class="even">
<td><span id="GI_NodeUpgradeProcess" class="anchor"></span>Node upgrade process</td>
<td>
<p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengupgradingk8sworkernode.htm">User-initiated</a><br />
Update note pool config, scale out to add nodes with new version, remove old nodes will cordon and drain. Alternatively, create new node pool and divert traffic (blue/green)</p>
</td>
<td><ul>
<li><p>Unmanaged node groups: <a href="https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html"><u>user-initiated and managed</u></a></p></li>
<li><p>Managed node groups: <a href="https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html"><u>user-initiated</u></a>; drains and replace nodes</p></li>
</ul></td>
<td><a href="https://docs.microsoft.com/en-us/azure/aks/upgrade-cluster#set-auto-upgrade-channel"><u>Automatically upgraded</u></a>; or <a href="https://docs.microsoft.com/en-us/azure/aks/upgrade-cluster#:%5c~:text=Upgrade%20an%20AKS%20cluster,-With%20a%20list&amp;text=During%20the%20upgrade%20process%2C%20AKS,the%20old%20node%20is%20deleted"><u>user-initiated</u></a>; AKS will drain and replace nodes</td>
<td><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/cluster-upgrades"><u>Automatically upgraded</u></a> during cluster maintenance window (default; can be turned off); can be user-initiated; drains and replaces nodes</td>
</tr>
<tr class="odd">
<td><span id="GI_NodeOS" class="anchor"></span>Node OS</td>
<td><ul>
<li><p><strong>Supported Images</strong> for worker nodes (<a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Reference/contengimagesshapes.htm">source</a>)<br />
*new images added regularly</p>
<ul>
<li><p><strong>Oracle Linux</strong> (<a href="#Note_GI_NodeOS_01"><strong>note</strong></a>)</p></li>
<li><p><strong>OKE images (<a href="#Note_GI_NodeOS_02">note</a>)</strong></p></li>
<li><p><em><strong>Looking for Windows? <a href="https://bit.ly/odevrel_slack">Let us know!</a></strong></em></p></li>
</ul></li>
</ul></td>
<td><p><strong>Linux:</strong></p>
<ul>
<li><p><a href="https://docs.aws.amazon.com/eks/latest/userguide/launch-workers.html"><u>Amazon Linux 2</u></a> (default); Ubuntu (partner AMI)</p></li>
<li><p><a href="https://docs.aws.amazon.com/eks/latest/userguide/launch-node-bottlerocket.html"><u>Bottlerocket</u></a></p></li>
</ul>
<p><strong>Windows:</strong></p>
<ul>
<li><p><a href="https://docs.aws.amazon.com/eks/latest/userguide/windows-support.html"><u>Windows Server 2019</u></a></p></li>
</ul></td>
<td><p><strong>Linux:</strong></p>
<ul>
<li><p><a href="https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#nodes-and-node-pools"><u>Ubuntu</u></a></p></li>
</ul>
<p><strong>Windows:</strong></p>
<ul>
<li><p><a href="https://azure.microsoft.com/en-us/blog/announcing-the-general-availability-of-windows-server-containers-and-private-clusters-for-azure-kubernetes-service/"><u>Windows Server 2019</u></a><br />
<em>must create AKS Cluster via CLI or PowerShell</em><u><br />
</u></p></li>
</ul></td>
<td><p><strong>Linux:</strong></p>
<ul>
<li>
<p>Container-Optimized OS (COS) (default), Ubuntu</p>
</li>
</ul>
<p><strong>Windows:</strong></p>
<ul>
<li>
<p><a href="https://cloud.google.com/kubernetes-engine/docs/how-to/creating-a-cluster-windows"><u>Windows Server 2019</u></a></p>
</li>
<li>
<p><a href="https://cloud.google.com/kubernetes-engine/docs/how-to/creating-a-cluster-windows"><u>Windows Server version 1909</u></a></p>
</li>
</ul></td>
</tr>
<tr class="even">
<td><span id="GI_ContainerRuntime" class="anchor"></span>Container runtime</td>
<td><ul>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengaboutk8sversions.htm">CRI-O</a></p></li>
</ul></td>
<td><ul>
<li><p>Docker (default &lt;= 1.23)</p></li>
<li><p><a href="https://aws.amazon.com/bottlerocket/"><u>containerd (default &gt;= 1.24)<br />
(also available through Bottlerocket)</u></a></p></li>
</ul></td>
<td><ul>
<li><p>Docker (default)</p></li>
<li><p><a href="https://azure.microsoft.com/en-ca/updates/azure-kubernetes-service-aks-support-for-containerd-runtime-is-in-preview/"><u>containerd</u></a></p></li>
</ul></td>
<td><ul>
<li><p>Docker (default)</p></li>
<li><p><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/using-containerd"><u>containerd</u></a></p></li>
<li><p><a href="https://cloud.google.com/blog/products/gcp/open-sourcing-gvisor-a-sandboxed-container-runtime"><u>gVisor</u></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><span id="GI_ControlPlaneHAoptions" class="anchor"></span>Control plane high availability options</td>
<td>Control plane is deployed to multiple, Oracle-managed control plane nodes which are distributed across different availability domains (where supported) or different fault domains.</td>
<td>Control plane is <a href="https://docs.aws.amazon.com/eks/latest/userguide/disaster-recovery-resiliency.html"><u>deployed across multiple Availability Zones (default)</u></a></td>
<td>Control plane components will be spread between <a href="https://docs.microsoft.com/en-us/azure/aks/availability-zones"><u>the number of zones defined by the Admin</u></a></td>
<td><p><strong>Zonal Clusters:</strong></p>

<p><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/types-of-clusters#single-zone_clusters"><u>Single Control Plane</u></a></p>

<p><strong>Regional Clusters:</strong></p>

<p><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/regional-clusters#about_regional_clusters"><u>Three Kubernetes control planes quorum</u></a></p>
</td>
</tr>
<tr class="even">
<td><span id="GI_ControlPlaneSLA" class="anchor"></span>Control plane SLA</td>
<td>
<p>99.95% SLO</p>
</td>
<td>
<p><a href="https://aws.amazon.com/eks/sla/"><u>99.95% (default)</u></a></p>
</td>
<td><ul>
<li><p><a href="https://techcommunity.microsoft.com/t5/apps-on-azure/aks-introduces-uptime-sla/ba-p/1350832"><u>99.95% (SLA backed)</u></a></p></li>
<li><p><a href="https://techcommunity.microsoft.com/t5/apps-on-azure/aks-introduces-uptime-sla/ba-p/1350832"><u>99.9% (non-SLA backed)</u></a></p></li>
</ul></td>
<td><ul>
<li><p><a href="https://cloud.google.com/kubernetes-engine/sla"><u>Zonal clusters: 99.95%</u></a></p></li>
<li><p><a href="https://cloud.google.com/kubernetes-engine/sla"><u>Regional clusters: 99.95%</u></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><span id="GI_UptimesSLA" class="anchor"></span>Uptimes SLA</td>
<td>
<p><a href="https://www.oracle.com/assets/paas-iaas-pub-cld-srvs-pillar-4021422.pdf">Compute SLA</a></p>

<ul>
<li><p>99.99 for regions with multiple Ads</p></li>
<li><p>99.95 for regions with one AD</p></li>
<li><p>99.9% for single instance</p></li>
</ul></td>
<td>
<p>guarantees 99.95% uptime</p>
</td>
<td>Offers 99.95% when availability zones are enabled, and 99.9% when disabled</td>
<td>
<p>GKE splits its managed Kubernetes clusters, offering 99.5% uptime for Zonal deployments and 99.95% for regional deployments.</p>
</td>
</tr>
<tr class="even">
<td><span id="GI_SLAfinanciallyBacked" class="anchor"></span>SLA financially-backed</td>
<td>
<p>Zero cost – not applicable</p>
</td>
<td>
<p><a href="https://aws.amazon.com/eks/sla"><u>Yes</u></a></p>
</td>
<td><a href="https://azure.microsoft.com/en-in/support/legal/sla/kubernetes-service/v1_1/"><u>Yes</u></a></td>
<td><a href="https://cloud.google.com/kubernetes-engine/sla"><u>Yes</u></a></td>
</tr>
<tr class="odd">
<td><span id="GI_GPUsupport" class="anchor"></span>GPU support</td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengrunninggpunodes.htm">Yes (NVIDIA)</a>; By selecting a compatible Oracle Linux GPU image, CUDA libraries are pre-installed. CUDA libraries for different GPUs do not have to be included in the application container.</td>
<td>
<p><a href="https://aws.amazon.com/about-aws/whats-new/2018/08/amazon-eks-supports-gpu-enabled-ec2-instances/"><u>Yes (NVIDIA)</u></a>; user must install device plugin in cluster</p>
</td>
<td><a href="https://docs.microsoft.com/en-us/azure/aks/gpu-cluster"><u>Yes (NVIDIA)</u></a>; user must install device plugin in cluster</td>
<td><p><a href="https://cloud.google.com/kubernetes-engine/docs/how-to/gpus"><u>Yes (NVIDIA)</u></a>; user must install device plugin in cluster</p>
<p><a href="https://cloud.google.com/blog/products/compute/announcing-google-cloud-a2-vm-family-based-on-nvidia-a100-gpu"><u>Compute Engine A2 VMs</u></a>; are also available</p></td>
</tr>
<tr class="even">
<td><span id="GI_CPlogCollection" class="anchor"></span>Container performance metrics</td>
<td><ul>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Reference/contengmetrics.htm">Default: On</a></p></li>
<li><p>Metrics and Alarms can be used to manage</p></li>
</ul></td>
<td><ul>
<li><p>Optional</p></li>
<li><p>Default: Off</p></li>
<li><p><em>Metrics are sent to</em> <a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Container-Insights-metrics-EKS.html"><em><strong><u>AWS CloudWatch Container Insights</u></strong></em></a></p></li>
</ul></td>
<td><ul>
<li><p>Optional</p></li>
<li><p>Default: Off</p></li>
<li><p><em>Metrics are sent to</em> <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/insights/container-insights-overview"><em><strong><u>Azure Monitor</u></strong></em></a></p></li>
</ul></td>
<td><ul>
<li><p>Optional</p></li>
<li><p>Default: Off</p></li>
<li><p><em>Metrics are sent to</em> <a href="https://cloud.google.com/monitoring/api/metrics_kubernetes"><em><strong><u>Stackdriver</u></strong></em></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><span id="GI_Monitoring" class="anchor"></span>Monitoring</td>
<td><ul>
<li><p><a href="https://docs.oracle.com/en/solutions/kubernetes-oke-logging-analytics/index.html#GUID-B90B5CC6-28BC-4F45-B4BF-CB416905C3D2">OCI logging analytics</a></p></li>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Reference/contengmetrics.htm">Container Engine for Kubernetes Metrics</a></p></li>
<li><p><a href="https://blogs.oracle.com/cloudnative/post/monitoring-oke-with-prometheus-and-grafana">Prometheus</a></p></li>
<li><p><a href="https://blogs.oracle.com/cloudnative/post/monitoring-oke-with-prometheus-and-grafana">Grafana</a></p></li>
<li><p><a href="https://www.datadoghq.com/blog/monitor-oracle-kubernetes-engine/">Datadog</a> and other 3<sup>rd</sup> party monitoring tools</p></li>
</ul></td>
<td><p><a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/ContainerInsights.html"><strong>CloudWatch Container Insights</strong></a><br />
Requires additional setup, metric selection, etc.</p>
<p>Also Supported:</p>
<ul>
<li><p>CloudWatch Agent</p></li>
<li><p>Fluent Bit</p></li>
<li><p>Fluentd</p></li>
<li><p>Prometheus</p></li>
<li><p>Other 3<sup>rd</sup> party tools</p></li>
</ul></td>
<td><p><strong>Azure Monitor</strong></p>
<p>Also supported:</p>
<ul>
<li><p>Fluentd</p></li>
<li><p>Prometheus</p></li>
<li><p>Other 3<sup>rd</sup> party tools</p></li>
</ul></td>
<td><p><strong>Kubernetes Engine Monitor</strong></p>
<p><a href="https://cloud.google.com/products/operations">Google Cloud’s operations suite</a> (formerly Stackdriver)</p>
<p>Also supported:</p>
<ul>
<li><p>Fluentd</p></li>
<li><p>Prometheus</p></li>
<li><p>Other 3<sup>rd</sup> party tools</p></li>
</ul></td>
</tr>
<tr class="even">
<td><span id="GI_ResourceMonitoring" class="anchor"></span>Node health monitoring</td>
<td><p>Self-healing – automatically provisions new worker nodes on failure to maintain cluster availability</p>
<p>Detect and repair capabilities also exist within autoscaling functionality.</p></td>
<td><a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Container-Insights-metrics-EKS.html">Container Insights metrics detect failed nodes.</a> Can trigger replace or allow autoscaling to replace node.</td>
<td><a href="https://docs.microsoft.com/en-us/azure/aks/node-auto-repair"><u>Auto repair</u></a> is now available. <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/insights/container-insights-analyze"><u>Node status monitoring is available</u></a>. Use <a href="https://docs.microsoft.com/en-us/azure/aks/cluster-autoscaler"><u>autoscaling rules</u></a> to shift workloads.</td>
<td>Worker node <a href="https://cloud.google.com/kubernetes-engine/docs/how-to/node-auto-repair"><u>auto-repair enabled</u></a> by default</td>
</tr>
<tr class="odd">
<td><span id="GI_Autoscaling" class="anchor"></span>Autoscaling</td>
<td><ul>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengautoscalingclusters.htm">Cluster Autoscaler</a> (<a href="https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md">FAQ</a>)</p></li>
<li><p><a href="https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/">Horizontal Pod Autoscaler</a></p></li>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengusingverticalpodautoscaler.htm">Vertical Pod Autoscaler</a></p></li>
<li><p><a href="https://kubesphere.io/docs/v3.3/installing-on-kubernetes/hosted-kubernetes/install-kubesphere-on-oke/">Third-party – Keda, KubeSphere</a> (HPA)</p></li>
</ul>
<p>“<strong>CA should handle up to 1000 nodes running 30 pods each.</strong> Our testing procedure is described <a href="https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/proposals/scalability_tests.md">here</a>.” (<a href="https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md">source</a>)</p></td>
<td><p><a href="https://docs.aws.amazon.com/eks/latest/userguide/autoscaling.html">Cluster Autoscaler</a> through:</p>
<ul>
<li><p>K8s CA</p></li>
<li><p>EC2 Auto scaling groups</p></li>
</ul></td>
<td><a href="https://learn.microsoft.com/en-us/azure/aks/cluster-autoscaler">Cluster autoscaler</a> native capabilities</td>
<td><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/cluster-autoscaler">Cluster autoscaler</a></td>
</tr>
<tr class="even">
<td><span id="GI_ServerlessComputing" class="anchor"></span>Serverless computing</td>
<td>Virtual Nodes coming soon: will deliver a complete, serverless Kubernetes experience.</td>
<td>Integrated with <a href="https://aws.amazon.com/fargate/"><strong>Fargate</strong></a>; customer can deploy pods as container instances rather than full VMs. Requires the use of <strong>Amazon Application Load Balancer</strong></td>
<td>Virtual nodes make serverless computing possible in AKS. Does not run separately from the available Kubernetes workloads. A customer can use virtual nodes by assigning particular workloads to them.</td>
<td><a href="https://cloud.google.com/anthos/run/docs/architecture-overview"><strong>Cloud Run</strong> for Anthos</a></td>
</tr>
<tr class="odd">
<td><span id="GI_Accessibility" class="anchor"></span>Accessibility</td>
<td>OCI has multiple realms: one commercial realm (with 34 regions) and multiple realms for Government Cloud: US Government Cloud <a href="https://docs.oracle.com/en-us/iaas/Content/General/Concepts/govfedramp.htm#Oracle_Cloud_Infrastructure_US_Government_Cloud_with_FedRAMP_Authorization"><u>FedRAMP authorized</u></a> and <a href="https://docs.oracle.com/en-us/iaas/Content/General/Concepts/govfeddod.htm#Oracle_Cloud_Infrastructure_US_Federal_Cloud_with_DISA_Impact_Level_5_Authorization"><u>IL5 authorized</u></a>, and <a href="https://docs.oracle.com/en-us/iaas/Content/General/Concepts/govuksouth.htm#Oracle_Cloud_Infrastructure_United_Kingdom_Government_Cloud"><u>United Kingdom Government Cloud</u></a></td>
<td><p>30 regions containing 96 Availability Zones. <em>Service availability may vary by region.</em></p>
<p>EKS is available on AWS GovCloud regions. AWS Fargate is NOT available in GovCloud regions.</p></td>
<td><p>Available in 57 of Azure’s 60 regions. <a href="https://learn.microsoft.com/en-us/azure/reliability/availability-zones-overview">Not all regions include availability zones</a></p>
<p>Available in GovCloud</p></td>
<td><p>Available in 35 regions;</p>
<p>No GovCloud support</p></td>
</tr>
<tr class="even">
<td><span id="GI_BareMetal" class="anchor"></span>Bare metal worker nodes</td>
<td><a href="https://www.oracle.com/cloud/cloud-native/container-engine-kubernetes/">Supports</a></td>
<td>Supports</td>
<td>Does not support</td>
<td>Does not support</td>
</tr>
<tr class="odd">
<td><span id="GI_WorkerNodeTypes" class="anchor"></span>Worker node types</td>
<td><p>Flex shapes, x86, ARM, HPC, GPU, clusters with mixed node types.</p>
<p>(<a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Reference/contengimagesshapes.htm">source</a>)</p></td>
<td><p>x86, ARM (Graviton), GPU</p>
<p>Specific node images required for various CPU / GPU combinations. (<a href="https://docs.aws.amazon.com/eks/latest/userguide/choosing-instance-type.html">source</a>)</p></td>
<td><p>x86, ARM, GPU</p>
<p>Minimum 2 vCPU per worker node. Provisioned node size cannot be changed without replacement.</p></td>
<td>x86, ARM (v1.24 or later, only), GPU</td>
</tr>
<tr class="even">
<td><span id="GI_ToolsForDevelopers" class="anchor"></span>Tools for developers</td>
<td><p>Oracle provided tools:</p>
<ul>
<li><p><a href="https://docs.public.oneportal.content.oci.oraclecloud.com/iaas/api/#/en/containerengine/">Container Engine API</a></p></li>
<li><p><a href="https://docs.public.oneportal.content.oci.oraclecloud.com/iaas/tools/oci-cli/latest/oci_cli_docs/cmdref/ce.html">Container Engine CLI</a></p></li>
<li><p><a href="https://docs.public.oneportal.content.oci.oraclecloud.com/iaas/Content/API/Concepts/sdks.htm">SDKs and CLI</a> (<strong>SDKs</strong>: Java, Python, TypeScript and JavaScript, .NET, Go, Ruby, PL/SQL)</p></li>
<li><p><a href="https://docs.public.oneportal.content.oci.oraclecloud.com/iaas/Content/API/Concepts/devcloudshellintro.htm">Cloud shell</a> / Code Editor</p></li>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/visualstudio_using.htm">Oracle Developer tools for Visual Studio</a></p></li>
</ul>
<p>Oracle customers can take full advantage of the K8s ecosystem - <a href="https://loft.sh/blog/kubernetes-statefulset-examples-and-best-practices/">Loft</a>, <a href="https://www.okteto.com/">Okteto</a>, <a href="https://blogs.oracle.com/developers/post/strengthen-your-developer-experience-and-deployment-velocity-with-oke-and-shipa-cloud">Shipa.io</a>, <a href="https://www.telepresence.io/docs/v1/discussion/overview/">Telepresence</a></p>
<ul>
<li><p>Helm/Helm charts</p></li>
<li><p><a href="https://www.ateam-oracle.com/post/continuous-deployments-with-skaffold-on-oracle-cloud-infrastructure-container-engine-for-kubernetes-oke">Skaffold</a></p></li>
<li><p><a href="https://oracle.github.io/learning-library/developer-library/cloud-native/oke-with-service-broker/workshops/oke-live-devops/freetier/?lab=kustomize">Kustomize</a> (<a href="https://oracle.github.io/learning-library/developer-library/cloud-native/oke-with-service-broker/workshops/oke-live-devops/freetier/?lab=skaffold">works with Skaffold</a>)</p></li>
<li><p><a href="https://docs.oracle.com/en-us/iaas/releasenotes/changes/0680c077-6857-4d7b-a51a-0ab245112572/">Terraform</a></p></li>
</ul></td>
<td><p>AWS Toolkit for VS Code supports ECR and ECS, but not EKS</p>
<p>AWS CloudShell</p>
<p>AWS CloudFormation</p>
<p>AWS SDKs and CLI</p>
<p>Full support for entire K8s ecosystem.</p></td>
<td><ul>
<li><p><strong>Kubernetes extension in VS Code</strong>.</p></li>
<li><p><a href="https://www.google.com/url?sa=t&amp;rct=j&amp;q=&amp;esrc=s&amp;source=web&amp;cd=&amp;cad=rja&amp;uact=8&amp;ved=2ahUKEwiysqvAouL5AhVRDkQIHVHjC9AQFnoECBMQAQ&amp;url=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fvisualstudio%2Fbridge%2Foverview-bridge-to-kubernetes&amp;usg=AOvVaw050ESgeAy8CRGAkOvEd2IO"><strong>Bridge to Kubernete</strong>s</a> which allows execution of local code as a service in a cluster. It also, replicates dependencies in a local environment.</p></li>
</ul></td>
<td><p>Google offers either Cloud Code or the VS Code extension to deploy, monitor, and control clusters directly in IDE.</p>
<p>Integrates with <strong>Cloud Run</strong> and <strong>Cloud Run for Anthos</strong>.</p></td>
</tr>
</tbody>
</table>

## **Service Limits**

Quick reference

- [Max clusters]
- [Max nodes per cluster]
- [Max nodes per node pool/group]
- [Max node pools/groups per cluster]
- [Max pods/node]

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 18%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Service/Provider</strong></th>
<th><strong>OKE</strong></th>
<th>EKS</th>
<th>AKS</th>
<th>GKE</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="SL_MaxClusters" class="anchor"></span>Max clusters</td>
<td><p><a href="https://docs.oracle.com/en-us/iaas/Content/General/Concepts/servicelimits.htm">15 clusters/region (Monthly Universal Credits) or 1 cluster/region (Pay-as-You-Go or Promo) by default</a></p>
<p>Limits can be increased through service request</p></td>
<td><a href="https://docs.aws.amazon.com/eks/latest/userguide/service-quotas.html"><u>100/region</u></a></td>
<td>5000 per subscription</td>
<td><a href="https://cloud.google.com/kubernetes-engine/quotas"><u>100/zone + 100 regional clusters</u></a></td>
</tr>
<tr class="even">
<td><span id="SL_MaxNodesCluster" class="anchor"></span>Max nodes per cluster</td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengoverview.htm">Each cluster you create can have a maximum of 1000 nodes</a></td>
<td><a href="https://docs.aws.amazon.com/eks/latest/userguide/service-quotas.html"><u>30 (Managed node groups) * 100 (Max nodes per group) = 3000</u></a></td>
<td><ul>
<li><p><a href="https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-kubernetes-service-limits"><u>5000 (Virtual Machine Scale Sets)</u></a></p></li>
<li><p>1000 (VM Availability Sets)</p></li>
</ul></td>
<td><ul>
<li><p><a href="https://cloud.google.com/kubernetes-engine/quotas"><u>15,000 nodes (v1.18 required)</u></a></p></li>
<li><p><a href="https://cloud.google.com/kubernetes-engine/quotas#limits_per_clus_er"><u>5000 nodes (v1.17 or lower)</u></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><span id="SL_MaxNodesNodePool" class="anchor"></span>Max nodes per node pool/group</td>
<td>1000</td>
<td>Managed node groups: 100</td>
<td><u><a href="https://docs.microsoft.com/en-us/azure/aks/quotas-skus-regions">100</a>0</u></td>
<td><a href="https://cloud.google.com/kubernetes-engine/quotas"><u>1000</u></a></td>
</tr>
<tr class="even">
<td><span id="SL_MaxNodePoolsCluster" class="anchor"></span>Max node pools/groups per cluster</td>
<td>No limit on number of node pools as long as total nodes per cluster does not exceed 1,000</td>
<td>Managed node groups: 30</td>
<td><a href="https://docs.microsoft.com/en-us/azure/aks/quotas-skus-regions"><u>100</u></a></td>
<td>Not documented</td>
</tr>
<tr class="odd">
<td><span id="SL_MaxPodsNode" class="anchor"></span>Max pods per node</td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengoverview.htm">110 pods/node</a></td>
<td><p><strong>Linux:</strong></p>
<ul>
<li><p><a href="https://medium.com/faun/aws-eks-and-pods-sizing-per-node-considerations-964b08dcfad3"><u>Varies by node instance type</u></a>: <em>((# of IPs per Elastic Network Interface - 1) * # of ENIs) + 2</em></p></li>
</ul>
<p><strong>Windows:</strong></p>
<ul>
<li><p><em># of IPs per ENI - 1</em></p></li>
</ul></td>
<td><ul>
<li><p><a href="https://docs.microsoft.com/en-us/azure/aks/quotas-skus-regions"><u>250 (Azure CNI, max, configured at cluster creation time)</u></a></p></li>
<li><p>110 (kubenet network)</p></li>
<li><p>30 (Azure CNI, default)</p></li>
</ul></td>
<td><a href="https://cloud.google.com/kubernetes-engine/docs/best-practices/scalability"><u>110 (default)</u></a></td>
</tr>
</tbody>
</table>

## **Networking and Security**

Quick reference

- [Network plugin/CNI]
- [Kubernetes RBAC]
- [Network policy]
- [Pod Security Admission Controller]
- [Private or public IP address for cluster Kubernetes API]
- [Private or Public IP addresses for nodes]
- [Pod-to-pod traffic encryption supported by provider]
- [Firewall for cluster Kubernetes API]
- [Read-only root filesystem on node]
- [General]

<table style="width:100%;">
<colgroup>
<col style="width: 20%" />
<col style="width: 29%" />
<col style="width: 17%" />
<col style="width: 15%" />
<col style="width: 17%" />
</colgroup>
<thead>
<tr class="header">
<th>Service/Provider</th>
<th><strong>OKE</strong></th>
<th>EKS</th>
<th>AKS</th>
<th>GKE</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="NS_NetworkPlugin" class="anchor"></span>Network plugin/CNI</td>
<td><ul>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengpodnetworking_topic-OCI_CNI_plugin.htm">OCI VCN-Native Pod Networking</a></p></li>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengpodnetworking_topic-flannel_CNI_plugin.htm">Flannel Overlay</a></p></li>
<li><p>Supports <a href="https://developer.oracle.com/tutorials/calico-with-oke/">Calico</a> network policy</p></li>
</ul></td>
<td><ul>
<li><p><a href="https://docs.aws.amazon.com/eks/latest/userguide/pod-networking.html">Amazon VPC Container Network Interface (CNI)</a></p></li>
<li><p><a href="https://projectcalico.docs.tigera.io/getting-started/kubernetes/managed-public-cloud/eks">Calico</a></p></li>
<li><p><a href="https://docs.aws.amazon.com/eks/latest/userguide/alternate-cni-plugins.html">Alternate compatible CNI plugins</a></p></li>
</ul></td>
<td><ul>
<li><p><a href="https://docs.microsoft.com/en-us/azure/aks/configure-azure-cni">Azure CNI kubenet</a></p></li>
<li><p><a href="https://projectcalico.docs.tigera.io/getting-started/kubernetes/managed-public-cloud/aks">Calico</a></p></li>
<li><p><a href="https://learn.microsoft.com/en-us/azure/aks/use-byo-cni?tabs=azure-cli">Alternate compatible CNI plugins</a></p></li>
</ul></td>
<td><ul>
<li><p><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/network-overview"><u>kubenet</u></a> (default)</p></li>
<li><p><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/network-overview"><u>Calico</u></a> (<a href="https://projectcalico.docs.tigera.io/getting-started/kubernetes/managed-public-cloud/gke">Additional Details</a>)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><span id="NS_RBAC" class="anchor"></span>Kubernetes RBAC</td>
<td><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengaboutaccesscontrol.htm"><strong>Not assigned by default</strong></a></p>
<p><em>Mutable after cluster creation</em></p>
<p>(<a href="#Note_NS_RBAC_01">note</a>; <a href="#Note_NS_RBAC_02">note</a>; <a href="#Note_NS_RBAC_03">note</a>)</p></td>
<td><p>Required</p>
<p><em>Immutable after cluster creation</em></p></td>
<td><p>Enabled by default</p>
<p><em>Immutable after cluster creation</em></p></td>
<td><p>Enabled by default</p>
<p><em>Mutable after cluster creation</em></p></td>
</tr>
<tr class="odd">
<td><span id="NS_NetworkPolicy" class="anchor"></span>Kubernetes Network Policy</td>
<td><ul>
<li><p>Not enabled by default</p></li>
<li><p>Calico can be manually installed at any time – can be installed alongside the CNI plugin (<a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengsettingupcalico.htm">source</a>)</p></li>
</ul></td>
<td><ul>
<li><p>Not enabled by default</p></li>
<li><p><a href="https://docs.aws.amazon.com/eks/latest/userguide/calico.html"><u>Calico can be manually installed at any time</u></a></p></li>
</ul></td>
<td><ul>
<li><p>Not enabled by default</p></li>
<li><p><a href="https://docs.microsoft.com/en-us/azure/aks/use-network-policies#create-an-aks-cluster-and-enable-network-policy"><u>Must be enabled at cluster creation time</u></a></p></li>
</ul></td>
<td><ul>
<li><p>Not enabled by default</p></li>
<li><p><a href="https://cloud.google.com/kubernetes-engine/docs/how-to/network-policy#enabling_network_policy_enforcement"><u>Can be enabled at any time</u></a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><span id="NS_PodSecurityPolicy" class="anchor"></span>Pod Security Admission Controller (PSA)</p>
<p>(<a href="#NS_PodSecurityAdmissionController">note</a>)</p></td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Reference/contengadmissioncontrollers.htm">PodSecurity Admission Controller</a> is supported by all OKE versions.</td>
<td><p>Enabled in EKS 1.23 by default.</p>
<p>(<a href="https://aws.amazon.com/blogs/containers/implementing-pod-security-standards-in-amazon-eks/">read more</a>)</p></td>
<td><p>Can be enabled in AKS clusters running K8s 1.23 or higher</p>
<p>(<a href="https://learn.microsoft.com/en-us/azure/aks/use-psa">read more</a>)</p></td>
<td><p>Available and enabled by default in GKE 1.25 (stable), 1.23 &amp; 1.24 (beta)</p>
<p>(<a href="https://cloud.google.com/kubernetes-engine/docs/how-to/migrate-podsecuritypolicy">read more</a>)</p></td>
</tr>
<tr class="odd">
<td><span id="NS_IPforCluster" class="anchor"></span>Private or public IP address for cluster Kubernetes API</td>
<td><ul>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengcreatingclusterusingoke_topic-Using_the_Console_to_create_a_Custom_Cluster_with_Explicitly_Defined_Settings.htm">Private</a> by default</p></li>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengclustersnodes.htm#processes">Optional public</a>, hybrid, or private</p><p>(<a href="#Note_NS_IPforCluster">note</a>)</p></li></ul>
</td>
<td><ul>
<li><p>Public by default</p></li>
<li><p><a href="https://docs.aws.amazon.com/eks/latest/userguide/cluster-endpoint.html"><u>Optional public, hybrid or private setup</u></a></p></li>
</ul></td>
<td><ul>
<li><p>Public by default</p></li>
<li><p><a href="https://docs.microsoft.com/en-us/azure/aks/private-clusters"><u>Private-only available where private link is supported</u></a></p></li>
</ul></td>
<td><ul>
<li><p>Public by default</p></li>
<li><p><a href="https://cloud.google.com/kubernetes-engine/docs/how-to/private-clusters#endpoints"><u>Optional public, hybrid or private setup</u></a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><span id="NS_IPforNodes" class="anchor"></span>Private or Public IP addresses for nodes</td>
<td><ul>
<li><p>Worker nodes can be public or private, depending on VCN Subnet configuration</p></li>
</ul></td>
<td><ul>
<li><p>Unmanaged node groups: <a href="https://aws.amazon.com/blogs/containers/upcoming-changes-to-ip-assignment-for-eks-managed-node-groups/"><u>Optional</u></a></p></li>
<li><p>Managed node groups: <a href="https://aws.amazon.com/blogs/containers/upcoming-changes-to-ip-assignment-for-eks-managed-node-groups/"><u>Optional</u></a></p></li>
</ul></td>
<td><ul>
<li><p>Public by default</p></li>
<li><p><a href="https://docs.microsoft.com/en-us/azure/aks/private-clusters"><u>Private can be enabled as well</u></a></p></li>
</ul></td>
<td><ul>
<li><p>Public by default</p></li>
<li><p><a href="https://cloud.google.com/kubernetes-engine/docs/how-to/private-clusters"><u>Private can be enabled as well</u></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><span id="NS_EncryptedPodTraffic" class="anchor"></span>Pod-to-pod traffic encryption supported by provider</td>
<td><ul>
<li><p>Yes, <a href="https://docs.oracle.com/en/solutions/oci-service-mesh-oke/index.html#GUID-C2C31164-55E2-442A-94D6-92EE5ADB2D86">OCI service mesh</a></p></li>
<li><p>And <a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengistio-intro-topic.htm">with Istio implemented</a></p></li>
</ul></td>
<td>Yes, with <a href="https://docs.aws.amazon.com/app-mesh/latest/userguide/getting-started-kubernetes.html">AWS App Mesh</a></td>
<td>Open Service Mesh as an add-on</td>
<td>Yes, with <a href="https://cloud.google.com/istio/docs/istio-on-gke/migrate-to-anthos-service-mesh">Anthos Service Mesh</a></td>
</tr>
<tr class="even">
<td><span id="NS_ClusterFirewall" class="anchor"></span>Firewall for cluster Kubernetes API</td>
<td><ul>
<li><p>CIDR allow list option</p></li>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengcidrblocks.htm">CIDR blocks and OKE</a></p></li>
</ul></td>
<td>CIDR allow list option</td>
<td>CIDR allow list option</td>
<td>CIDR allow list option</td>
</tr>
<tr class="odd">
<td><span id="NS_ROrootFS" class="anchor"></span>Read-only root filesystem on node</td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengusingpspswithoke.htm">Pod security policy required</a></td>
<td><a href="https://aws.amazon.com/blogs/opensource/using-pod-security-policies-amazon-eks-clusters/"><u>Pod security policy required</u></a></td>
<td><a href="https://docs.microsoft.com/en-us/azure/aks/policy-reference"><u>Azure policy required</u></a></td>
<td><ul>
<li><p><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/node-images#file_system_layout"><u>COS: default</u></a></p></li>
<li><p><a href="https://cloud.google.com/kubernetes-engine/docs/how-to/pod-security-policies"><u>Alternative: Pod security policy required</u></a></p></li>
</ul></td>
</tr>
</tbody>
</table>

<span id="NS_General" class="anchor"></span>

## Container Image Services

Quick Reference

- [Image repository service]
- [Supported formats]
- [Access security]
- [Supported Image Signing]
- [Supports Immutable Image Tags]
- [Image scanning service]
- [Registry SLA]
- [Georedundancy]

<table style="width:100%;">
<colgroup>
<col style="width: 20%" />
<col style="width: 17%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th><strong>OKE</strong></th>
<th>EKS</th>
<th>AKS</th>
<th>GKE</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="CIS_ImageRespositoryService" class="anchor"></span>Image repository service</td>
<td><a href="https://www.oracle.com/cloud/cloud-native/container-registry/">OCI Container Registry</a></td>
<td>ECR (Elastic Container Registry)</td>
<td>ACR (Azure Container Registry)</td>
<td>AR (Artifact Registry)</td>
</tr>
<tr class="even">
<td><span id="CIS_SupportedFormats" class="anchor"></span>Supported formats</td>
<td><ul>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/Registry/Concepts/registryoverview.htm">Docker images</a></p></li>
<li><p>OCI Specifications</p></li>
<li><p>Helm charts</p></li>
<li><p><a href="https://docs.docker.com/registry/spec/manifest-v2-2/">Docker Image Manifest V2, Schema 2</a> (<a href="https://docs.oracle.com/en-us/iaas/releasenotes/changes/a3a9f4e6-76bf-4a5a-b227-d46a76cbfba2/">source</a>)</p></li>
</ul></td>
<td><ul>
<li><p><a href="https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-manifest-formats.html"><u>Docker Image Manifest V2, Schema 1</u></a></p></li>
<li><p><a href="https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-manifest-formats.html"><u>Docker Image Manifest V2, Schema 2</u></a></p></li>
<li><p><a href="https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-manifest-formats.html"><u>Open Container Initiative (OCI) Specifications</u></a></p></li>
<li><p><a href="https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-manifest-formats.html"><u>Helm Charts</u></a></p></li>
</ul></td>
<td><ul>
<li><p><a href="https://docs.microsoft.com/en-us/azure/container-registry/container-registry-image-formats"><u>Docker Image Manifest V2, Schema 1</u></a></p></li>
<li><p><a href="https://docs.microsoft.com/en-us/azure/container-registry/container-registry-image-formats"><u>Docker Image Manifest V2, Schema 2</u></a></p></li>
<li><p><a href="https://docs.microsoft.com/en-us/azure/container-registry/container-registry-image-formats"><u>Open Container Initiative (OCI) Specifications</u></a></p></li>
<li><p><a href="https://docs.microsoft.com/en-us/azure/container-registry/container-registry-image-formats"><u>Helm Charts</u></a></p></li>
</ul></td>
<td><ul>
<li><p><a href="https://cloud.google.com/container-registry/docs/image-formats"><u>Docker Image Manifest V2, Schema 1</u></a></p></li>
<li><p><a href="https://cloud.google.com/container-registry/docs/image-formats"><u>Docker Image Manifest V2, Schema 2</u></a></p></li>
<li><p><a href="https://cloud.google.com/container-registry/docs/image-formats"><u>Open Container Initiative (OCI) Specifications</u></a></p></li>
<li><p><a href="https://cloud.google.com/artifact-registry/docs/java/quickstart"><u>Maven and Gradle</u></a></p></li>
<li><p><a href="https://cloud.google.com/artifact-registry/docs/nodejs/quickstart"><u>npm</u></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><span id="CIS_AccessSecurity" class="anchor"></span>Access security</td>
<td><ul>
<li><p>Permissions managed by Oracle <a href="https://www.oracle.com/security/identity-management/">IAM</a></p></li>
<li><p>Can be applied at the repository level</p></li>
<li><p>Network endpoint is public by default</p></li>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/Identity/Tasks/managingnetworksources.htm">Network Source can be limited to specific IP addresses / ranges</a></p></li>
</ul></td>
<td><ul>
<li><p>Permissions managed by AWS IAM</p></li>
<li><p><a href="https://docs.aws.amazon.com/AmazonECR/latest/userguide/security_iam_id-based-policy-examples.html"><u>Permissions can be applied at repository level</u></a></p></li>
<li><p>Network endpoint is public by default</p></li>
<li><p><a href="https://docs.aws.amazon.com/AmazonECR/latest/userguide/vpc-endpoints.html"><u>Network endpoint can be limited to specific VPCs</u></a></p></li>
</ul></td>
<td><ul>
<li><p>Permissions managed by Azure RBAC</p></li>
<li><p><a href="https://docs.microsoft.com/en-us/azure/container-registry/container-registry-repository-scoped-permissions"><u>Can be applied at repository level</u></a> (<em>preview</em>)</p></li>
<li><p>Network endpoint is public by default</p></li>
<li><p><a href="https://docs.microsoft.com/en-us/azure/container-registry/container-registry-vnet"><u>Network endpoint can be limited to specific VNets</u></a> (<em>preview</em>)</p></li>
</ul></td>
<td><ul>
<li><p>Permissions managed by GCP IAM</p></li>
<li><p><a href="https://cloud.google.com/container-registry/docs/access-control#service-account"><u>Permissions can only be applied at registry level</u></a></p></li>
<li><p>Network endpoint is public by default</p></li>
<li><p><a href="https://cloud.google.com/container-registry/docs/securing-with-vpc-sc"><u>Network access for GCR registries can be limited to specific VPCs with service perimeters</u></a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><span id="CIS_SupportedImageSigning" class="anchor"></span>Supports image signing</td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/Registry/Tasks/registrysigningimages_topic.htm">Yes</a></td>
<td>No</td>
<td><a href="https://cloud.google.com/container-registry/docs/securing-with-vpc-sc"><u>Yes</u></a></td>
<td>Yes, with <a href="https://cloud.google.com/binary-authorization/docs/overview"><u>Binary Authorization</u></a> and <a href="https://cloud.google.com/binary-authorization/docs/creating-attestations-voucher"><u>Voucher</u></a></td>
</tr>
<tr class="odd">
<td><span id="CIS_SupportsImmutableImageTags" class="anchor"></span>Supports immutable image tags</td>
<td><p><a href="https://docs.oracle.com/en-us/iaas/Content/artifacts/overview.htm">Yes</a>, and supports:</p>
<ul>
<li><p>Identifying them with secure hashes</p></li>
<li><p>Adding versions</p></li>
<li><p>Controlling visibility and permissions</p></li>
</ul></td>
<td><a href="https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-tag-mutability.html"><u>Yes</u></a></td>
<td><a href="https://azure.microsoft.com/en-ca/updates/azure-container-registry-tag-locking-policy-is-now-generally-available/"><u>Yes</u></a>, and it <a href="https://docs.microsoft.com/en-us/azure/container-registry/container-registry-image-lock"><u>supports the locking of images and repositories</u></a></td>
<td>No</td>
</tr>
<tr class="even">
<td><span id="CIS_ImageScanningService" class="anchor"></span>Image scanning service</td>
<td><p><a href="https://docs.oracle.com/en-us/iaas/scanning/using/managing-image-targets.htm">Yes</a>, <a href="https://www.oracle.com/security/cloud-security/vulnerability-scanning-service/"><strong>Oracle Vulnerability Scanning Service</strong></a></p>
<p>(<a href="#Note_CIS_ImageScanningService_01">note</a>)</p></td>
<td>Yes, <a href="https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html"><u>free service: OS packages only</u></a></td>
<td>Yes, <a href="https://docs.microsoft.com/en-us/azure/security-center/azure-container-registry-integration"><u>paid service</u></a>: Uses the <a href="https://www.qualys.com/apps/container-security/"><u>Qualys scanner</u></a> in a sandbox to check for vulnerabilities</td>
<td>Yes, <a href="https://cloud.google.com/container-registry/docs/vulnerability-scanning"><u>paid Service: OS packages only</u></a></td>
</tr>
<tr class="odd">
<td><span id="CIS_RegistrySLA" class="anchor"></span>Registry SLA</td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/General/Reference/servicelevelobjectives.htm">99.9% SLO</a></td>
<td><a href="https://aws.amazon.com/ecr/sla/"><u>99.9%; financially backed</u></a></td>
<td><a href="https://azure.microsoft.com/en-us/support/legal/sla/container-registry/v1_1/"><u>99.9%; financially backed</u></a></td>
<td><a href="https://cloud.google.com/container-registry/sla"><u>None</u></a></td>
</tr>
<tr class="even">
<td><span id="CIS_GeoRedundancy" class="anchor"></span>Geo-Redundancy</td>
<td>No</td>
<td>Yes, <a href="https://aws.amazon.com/blogs/containers/cross-region-replication-in-amazon-ecr-has-landed/"><u>configurable</u></a></td>
<td>Yes, <a href="https://docs.microsoft.com/en-us/azure/container-registry/container-registry-geo-replication"><u>configurable as part of the premium service</u></a></td>
<td>Yes, by default</td>
</tr>
</tbody>
</table>

## Notes

### General Information

#### [Node OS]

-   <span id="Note_GI_NodeOS_01" class="anchor"></span>**(note 1)** some, but not all, of the latest Oracle Linux images provided by Oracle Cloud Infrastructure

**Note:** “Docker is not included in Oracle Linux 8 images. Instead, in node pools running Kubernetes 1.20.x and later, Container Engine for Kubernetes installs and uses the CRI-O container runtime and the crictl CLI (for more information, see Notes about Container Engine for Kubernetes Support for Kubernetes Version 1.20).”

-   <span id="Note_GI_NodeOS_02" class="anchor"></span>**(note 2)** OKE images are provided by Oracle and built on top of platform images. OKE images are optimized for use as worker node base images, with all the necessary configurations and required software

-   **(note 3)** Custom images are provided by you and can be based on both supported platform images and OKE images. Custom images contain Oracle Linux operating systems, along with other customizations, configuration, and software that were present when you created the image.

### Service Limits

### Networking and Security

#### [RBAC][Kubernetes RBAC]

-   <span id="Note_NS_RBAC_01" class="anchor"></span>**(note 1)** “**By default, users are not assigned any Kubernetes RBAC roles (or clusterroles).** Before attempting to create a new role (or clusterrole), you must be assigned an appropriately privileged role (or clusterrole). A number of such roles and clusterroles are always created by default, including the cluster-admin clusterrole (for a full list, see Default Roles and Role Bindings in the Kubernetes documentation). The cluster-admin clusterrole essentially confers super-user privileges. A user granted the cluster-admin clusterrole can perform any operation across all namespaces in a given cluster.” ([source][RBAC_source1])

-   <span id="Note_NS_RBAC_02" class="anchor"></span>**(note 2)** “For most operations on Kubernetes clusters created and managed by Container Engine for Kubernetes, **Oracle Cloud Infrastructure Identity and Access Management (IAM)** provides access control.” ([source][RBAC_source1])

-   <span id="Note_NS_RBAC_03" class="anchor"></span>**(note 3)** “In addition to IAM, the Kubernetes RBAC Authorizer can enforce additional fine-grained access control for users on specific clusters via Kubernetes RBAC roles and clusterroles.” ([source][RBAC_source1])

#### [Pod Security][Pod Security Admission Controller]

<span id="NS_PodSecurityAdmissionController" class="anchor"></span>Pod Security

-   **(note 1) Kubernetes Pod Security Policy will be deprecated starting with Kubernetes version 1.21, and will be removed entirely in version 1.25.** Recommended best practice is to migrate pod security policy to pod security admission controller before the deprecation deadline.

#### [Private or public IP Address for Clusters][Private or public IP address for cluster Kubernetes API]

-   <span id="Note_NS_IPforCluster" class="anchor"></span>**(note 1)** “You access the Kubernetes API on the cluster control plane through an endpoint hosted in a subnet of your VCN. This Kubernetes API endpoint subnet can be a private or public subnet. If you specify a public subnet for the Kubernetes API endpoint, you can optionally assign a public IP address to the Kubernetes API endpoint (in addition to the private IP address). You control access to the Kubernetes API endpoint subnet using security rules defined for security lists or network security groups.”

### Container Image Services

#### [Image scanning service][]

-   <span id="Note_CIS_ImageScanningService_01" class="anchor"></span>**(note 1)** “Create and manage container image targets and to assign them to container image scan recipes. A container image target is a collection of repositories in [Container Registry] that you want scanned for security vulnerabilities.”

## **References**

-   ([StackRox]) EKS vs GKE vs AKS - Evaluating Kubernetes in the Cloud

-   ([itoutposts]) Kubernetes Engines Compared: Full Guide

-   ([veritis]) EKS Vs. AKS Vs. GKE: Which is the right Kubernetes platform for you?

-   ([kloia]) Comparison of Kubernetes Engines

  [reach us any time on Slack!]: https://bit.ly/odevrel_slack
  [Currently supported Kubernetes version(s)]: #GI_CurrentKs8Version
  [\# of supported minor version releases]: #GI_SupportedMinorVersions
  [Original GA release date]: #GI_ReleaseDate
  [Pricing]: #GI_Pricing
  [CNCF Kubernetes Conformance]: #GI_CNCFconformance
  [CLI support]: #GI_CNCFcertifiedVersion
  [Control-plane upgrade process]: #GI_ControlPlaneUpgradeProcess
  [Node upgrade process]: #GI_NodeUpgradeProcess
  [Node OS]: #GI_NodeOS
  [Container runtime]: #GI_ContainerRuntime
  [Control plane high availability options]: #GI_ControlPlaneHAoptions
  [Control plane SLA]: #GI_ControlPlaneSLA
  [Uptimes SLA]: #GI_UptimesSLA
  [SLA financially-backed]: #GI_SLAfinanciallyBacked
  [GPU support]: #GI_GPUsupport
  [Container performance metrics]: #GI_CPlogCollection
  [Monitoring]: #GI_Monitoring
  [Node health monitoring]: #GI_ResourceMonitoring
  [Autoscaling]: #GI_Autoscaling
  [Serverless computing]: #GI_ServerlessComputing
  [Accessibility]: #GI_Accessibility
  [Bare metal clusters]: #GI_BareMetal
  [Worker node types]: #GI_WorkerNodeTypes
  [Tools for developers]: #GI_ToolsForDevelopers
  [Max clusters]: #SL_MaxClusters
  [Max nodes per cluster]: #SL_MaxNodesCluster
  [Max nodes per node pool/group]: #SL_MaxNodesNodePool
  [Max node pools/groups per cluster]: #SL_MaxNodePoolsCluster
  [Max pods/node]: #SL_MaxPodsNode
  [Network plugin/CNI]: #NS_NetworkPlugin
  [Kubernetes RBAC]: #NS_RBAC
  [Network policy]: #NS_NetworkPolicy
  [Pod Security Admission Controller]: #NS_PodSecurityPolicy
  [Private or public IP address for cluster Kubernetes API]: #NS_IPforCluster
  [Private or Public IP addresses for nodes]: #NS_IPforNodes
  [Pod-to-pod traffic encryption supported by provider]: #NS_EncryptedPodTraffic
  [Firewall for cluster Kubernetes API]: #NS_ClusterFirewall
  [Read-only root filesystem on node]: #NS_ROrootFS
  [General]: #NS_General
  [Image repository service]: #CIS_ImageRespositoryService
  [Supported formats]: #CIS_SupportedFormats
  [Access security]: #CIS_AccessSecurity
  [Supported Image Signing]: #CIS_SupportedImageSigning
  [Supports Immutable Image Tags]: #CIS_SupportsImmutableImageTags
  [Image scanning service]: #CIS_ImageScanningService
  [Registry SLA]: #CIS_RegistrySLA
  [Georedundancy]: #CIS_GeoRedundancy
  [RBAC_source1]: https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengaboutaccesscontrol.htm
  [Container Registry]: https://www.oracle.com/cloud/cloud-native/container-registry/
  [StackRox]: https://www.stackrox.io/blog/eks-vs-gke-vs-aks-jan2021/
  [itoutposts]: https://itoutposts.com/blog/kubernetes-engines-compared-full-guide/
  [veritis]: https://www.veritis.com/blog/eks-vs-aks-vs-gke-which-is-the-right-kubernetes-platform-for-you/
  [kloia]: https://www.kloia.com/blog/comparison-of-the-kubernetes-engines
