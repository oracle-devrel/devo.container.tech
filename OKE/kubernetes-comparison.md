---
title: Kubernetes: A comparison of managed engines
description: An extensive comparison of the four most prolific managed Kubernetes offerings.
author:
  name: Eli Schilling
  bio: Oracle DevRel Advocate, cloud native app dev and DevOps.
  github: https://github.com/oracle-devrel
  youtube: https://www.youtube.com/c/oracledevs/playlists
  email: eli.schilling@oracle.com
parent: [tutorials]
categories: [cloudapps, clouddev, modernize, enterprise]
date: 2023-01-23 08:00
modified: 2023-08-01 08:00

---

## **General Information**

This document contains an extensive, though not exhaustive comparison of the four most prolific managed Kubernetes offerings: Oracle Container Engine for Kubernetes (OKE), Amazon Elastic Kubernetes Service (EKS), Azure Kubernetes Service (AKS), and Google Kubernetes Engine (GKE). The comparison was developed with input from the community and will continue to be revised as the technology changes.

Last modified August 1st, 2023, this document will be updated regularly to ensure consistent and relevant information is made available. Should you have any questions or wish to contribute feedback, you may [reach us any time on Slack!]

Quick reference

- [Supported Kubernetes version(s)]
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
- [Preemptible capacity]
- [Cluster addons]

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
<td><span id="GI_CurrentKs8Version" class="anchor"></span>Supported Kubernetes version(s)
<p>(<a href="#Note_GI_K8s_Versions"><strong>note</strong></a>)</td>
<td><p>Container Engine for Kubernetes supports three versions of Kubernetes for new clusters. For a minimum of 30 days after the announcement of support for a new Kubernetes version, Container Engine for Kubernetes continues to support the fourth, oldest available Kubernetes version. After that time, the older Kubernetes version ceases to be supported.</p>
<p>(<a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengaboutk8sversions.htm">source</a>)</p></td>
<td><p>EKS is committed to supporting at least four production-ready versions of Kubernetes at any given time. We will announce the end of support date of a given Kubernetes minor version at least 60 days before the end of support date. Because of the Amazon EKS qualification and release process for new Kubernetes versions, the end of support date of a Kubernetes version on Amazon EKS will be on or after the date that the Kubernetes project stops supporting the version upstream.</p>
<p>(<a href="https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-versions.html">source</a>)</p></td>
<td><p>AKS defines a generally available (GA) version as a version available in all regions and enabled in all SLO or SLA measurements. AKS supports three GA minor versions of Kubernetes:

* The latest GA minor version released in AKS (which we'll refer to as N).
* Two previous minor versions.
  * Each supported minor version also supports a maximum of two stable patches.</p>
<p>(<a href="https://docs.microsoft.com/en-us/azure/aks/supported-kubernetes-versions?tabs=azure-cli">source</a>)</p></td>
<td><p>Based on the current Kubernetes OSS community version support policy, GKE plans to maintain supported minor versions for 14 months, including the 12 months after the release in the Regular channel, followed by a 2-month maintenance period. During the maintenance period, no new node pool creations will be allowed for a maintenance version, but existing node pools that run a maintenance version will continue to remain in operation.</p>
<p><a href="https://cloud.google.com/kubernetes-engine/versioning">source</a>)</p></td>
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
<td><a href="https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm"><u>$0.10 per hour</u></a> per cluster + standard costs of Compute instances and other resources.<p>Basic Cluster option available for free</td>
<td><a href="https://aws.amazon.com/eks/pricing/"><u>$0.10/hour (USD)</u></a> per cluster + standard costs of EC2 instances and other resources</td>
<td><a href="https://azure.microsoft.com/en-ca/pricing/details/kubernetes-service/"><u>$0.10 per hour</u></a> per cluster + Standard costs of node VMs and other resources. Free tier available for exploration.</td>
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
<td>Full support of Kubernetes clusters; <a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengaccessingclusterkubectl.htm">kubectl</a> support</td>
<td>Full support of Kubernetes clusters; kubectl support</td>
<td>Full support of Kubernetes clusters; kubectl support</td>
<td>Full support of Kubernetes clusters; kubectl support</td>
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
Update node pool config, scale out to add nodes with new version, remove old nodes will cordon and drain. Alternatively, create new node pool and divert traffic (blue/green)</p>
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
<td>
<p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengaboutk8sversions.htm">CRI-O</a></p></li>
</td>
<td>
<p><a href="https://aws.amazon.com/bottlerocket/"><u>containerd (default &gt;= 1.24)<br />
(also available through Bottlerocket)</u></a></p>
</td>
<td>
<p><a href="https://learn.microsoft.com/en-us/azure/aks/cluster-configuration">containerd</a></p>
</ul></td>
<td>
<p><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/using-containerd"><u>containerd</u></a></p>
</td>
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
<p><a href="https://www.oracle.com/content/published/api/v1.1/assets/CONT95B931480DF242229DF530A64F0D0245/native/Oracle%20PaaS%20and%20IaaS%20Public%20Cloud%20Services%20Pillar%20Document.pdf?cb=_cache_a99f&channelToken=117bec9b3b4e4e90a1c4c9069d210baf&download=false"><u>99.95% SLA</u></a></p>
</td>
<td>
<p><a href="https://aws.amazon.com/eks/sla/"><u>99.95% (default)</u></a></p>
</td>
<td><ul>
<li><p><a href="https://techcommunity.microsoft.com/t5/apps-on-azure/aks-introduces-uptime-sla/ba-p/1350832"><u>99.95% (SLA backed)</u></a></p></li>
<li><p><a href="https://techcommunity.microsoft.com/t5/apps-on-azure/aks-introduces-uptime-sla/ba-p/1350832"><u>99.9% (non-SLA backed)</u></a></p></li>
</ul></td>
<td><ul>
<li><p><a href="https://cloud.google.com/kubernetes-engine/sla"><u>Zonal clusters: 99.5%</u></a></p></li>
<li><p><a href="https://cloud.google.com/kubernetes-engine/sla"><u>Regional clusters: 99.95%</u></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><span id="GI_UptimesSLA" class="anchor"></span>Uptimes SLA</td>
<td>
<p><a href="https://www.oracle.com/assets/paas-iaas-pub-cld-srvs-pillar-4021422.pdf">Compute SLA</a></p>

<ul>
<li><p>99.99% for regions with multiple ADs</p></li>
<li><p>99.95% for regions with one AD</p></li>
<li><p>99.9% for single instance</p></li>
</ul></td>
<td>
<p>Guarantees 99.95% uptime</p>
</td>
<td>Offers 99.95% when availability zones are enabled, and 99.9% when disabled</td>
<td>
<p>GKE splits its managed Kubernetes clusters, offering 99.5% uptime for Zonal deployments and 99.95% for regional deployments.</p>
</td>
</tr>
<tr class="even">
<td><span id="GI_SLAfinanciallyBacked" class="anchor"></span>SLA financially-backed</td>
<td>
<p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengcomparingenhancedwithbasicclusters_topic.htm"><u>Yes</u></a></p>
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
<td><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengworkingwithvirtualnodes.htm">Virtual Nodes</a> and Virtual Node pools provide a serverless Kubernetes experience with per-Pod billing.</td>
<td><a href="https://aws.amazon.com/fargate/">AWS Fargate</a> removes the need to provision and manage servers.</td>
<td><a href="https://learn.microsoft.com/en-us/azure/aks/virtual-nodes">AKS Virtual Nodes</a> are heavily dependent on <a href="https://learn.microsoft.com/en-us/azure/container-instances/container-instances-overview">Azure Container Instances'</a> feature set.</td>
<td><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/autopilot-overview">GKE Autopilot</a> provides a serverless Kubernetes experience.</td>
</tr>
<tr class="odd">
<td><span id="GI_Accessibility" class="anchor"></span>Accessibility</td>
<td>OCI has multiple realms: one <a href="https://www.oracle.com/cloud/public-cloud-regions/">commercial realm</a> (with 44 regions) and multiple realms for Government Cloud: US Government Cloud <a href="https://docs.oracle.com/en-us/iaas/Content/General/Concepts/govfedramp.htm#Oracle_Cloud_Infrastructure_US_Government_Cloud_with_FedRAMP_Authorization"><u>FedRAMP authorized</u></a> and <a href="https://docs.oracle.com/en-us/iaas/Content/General/Concepts/govfeddod.htm#Oracle_Cloud_Infrastructure_US_Federal_Cloud_with_DISA_Impact_Level_5_Authorization"><u>IL5 authorized</u></a>, and <a href="https://docs.oracle.com/en-us/iaas/Content/General/Concepts/govuksouth.htm#Oracle_Cloud_Infrastructure_United_Kingdom_Government_Cloud"><u>United Kingdom Government Cloud</u></a></td>
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
<td><p>x86, ARM*, GPU</p>
<p><i>*ARM supported only on v1.24 or later and only in 3 regions:<li>us-central1 (Iowa)</li><li>europe-west4 (Netherlands)</li><li>asia-southeast1 (Singapore)</li></i></td>
</tr>
<tr class="even">
<td><span id="GI_Preemptible_capacity" class="anchor"></span>Preemptible Capacity</td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengusingpreemptiblecapacity.htm">Supports</a></td>
<td>EKS supports use of <a href="https://aws.amazon.com/about-aws/whats-new/2020/12/amazon-eks-support-ec2-spot-instances-managed-node-groups/">Spot Instances</a> within managed node groups.</td>
<td><a href="https://learn.microsoft.com/en-us/azure/aks/spot-node-pool">Azure Spot node pools</a> can be used.</td>
<td><a href="https://cloud.google.com/kubernetes-engine/docs/how-to/preemptible-vms">Supports</a></td>
</tr>
<tr class="odd">
<td><span id="GI_Cluster_Addons" class="anchor"></span>Cluster Add-on Management</td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengconfiguringclusteraddons.htm">Full lifecycle management for available cluster add-ons</a></td>
<td><a href="https://docs.aws.amazon.com/eks/latest/userguide/eks-add-ons.html">Full lifecycle management for available cluster add-ons</a></td>
<td><a href="https://learn.microsoft.com/en-us/azure/aks/integrations">Full lifecycle management for available cluster add-ons</a></td>
<td>Numerous add-ons available, though documentation is limited.</td>
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
<td><p><a href="https://docs.oracle.com/en-us/iaas/Content/General/Concepts/servicelimits.htm">15 clusters/region</a> (Monthly Universal Credits) or 1 cluster/region (Pay-as-You-Go or Promo) by default</p>
<p>Limits can be increased through service request</p></td>
<td><a href="https://docs.aws.amazon.com/eks/latest/userguide/service-quotas.html"><u>100/region</u></a></td>
<td>5000 per subscription</td>
<td>100 <a href="https://cloud.google.com/kubernetes-engine/docs/concepts/types-of-clusters#zonal_clusters">zonal clusters</a> per zone, plus 100 <a href="https://cloud.google.com/kubernetes-engine/docs/concepts/types-of-clusters#regional_clusters">regional clusters</a> per region</td>
</tr>
<tr class="even">
<td><span id="SL_MaxNodesCluster" class="anchor"></span>Max nodes per cluster</td>
<td><li>1000 per basic cluster</li><li>2000 per enhanced cluster</li><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengoverview.htm">source</a></td>
<td><p>450 nodes/node group * 30 node groups/cluster = 13,500 nodes/cluster</p><a href="https://docs.aws.amazon.com/eks/latest/userguide/service-quotas.html">source</a></td>
<td><ul>
<li><p><a href="https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-kubernetes-service-limits"><u>5000 (Virtual Machine Scale Sets)</u></a></p></li>
<li><p>1000 (VM Availability Sets)</p></li>
</ul></td>
<td><p><a href="https://cloud.google.com/kubernetes-engine/quotas">15,000 nodes</a></p> (v1.18 and newer)</p>
</ul></td>
</tr>
<tr class="odd">
<td><span id="SL_MaxNodesNodePool" class="anchor"></span>Max nodes per node pool/group</td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/General/Concepts/servicelimits.htm">1000</a></td>
<td>Managed node groups: 100</td>
<td><u><a href="https://docs.microsoft.com/en-us/azure/aks/quotas-skus-regions">1000</a></u></td>
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
<td><li>110 pods/managed node</li><li>500 pods/virtual node</li>
<a href=https://docs.oracle.com/en-us/iaas/Content/General/Concepts/servicelimits.htm>source></a></td>
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
<td><li>256 for Standard cluster</li><li>32 fro Autopilot cluster</li><a href="https://cloud.google.com/kubernetes-engine/docs/best-practices/scalability">source</a></td>
</tr>
</tbody>
</table>

## **Networking and Security**

Quick reference

- [Network plugin/CNI]
- [Kubernetes RBAC]
- [Workload Identity]
- [Network policy]
- [Pod Security Admission Controller]
- [Private or public IP address for cluster Kubernetes API]
- [Private or Public IP addresses for nodes]
- [Pod-to-pod traffic encryption supported by provider]
- [Firewall for cluster Kubernetes API]
- [Read-only root filesystem on node]
- [External secrets management]
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
<td><span id="NS_WorkloadIdentity" class="anchor"></span>Workload Identity (Pod-level authorization)</td>
<td><a href="https://blogs.oracle.com/cloud-infrastructure/post/oke-workload-identity-greater-control-access">OKE Workload Identity</a></td>
<td><a href="https://docs.aws.amazon.com/eks/latest/userguide/pod-configuration.html">Kubernetes service accounts in EKS</a></td>
<td><a href="https://learn.microsoft.com/en-us/azure/aks/workload-identity-overview">Azure AD workload identity (preview)</a></td>
<td><a href="https://cloud.google.com/kubernetes-engine/docs/how-to/workload-identity">GKE Workload Identity</a></td>
</tr>
<tr class="even">
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
<tr class="odd">
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
<tr class="even">
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
<tr class="odd">
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
<tr class="even">
<td><span id="NS_EncryptedPodTraffic" class="anchor"></span>Pod-to-pod traffic encryption supported by provider</td>
<td><ul>
<li><p>Yes, <a href="https://docs.oracle.com/en/solutions/oci-service-mesh-oke/index.html#GUID-C2C31164-55E2-442A-94D6-92EE5ADB2D86">OCI service mesh</a></p></li>
<li><p>And <a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengistio-intro-topic.htm">with Istio implemented</a></p></li>
</ul></td>
<td>Yes, with <a href="https://docs.aws.amazon.com/app-mesh/latest/userguide/getting-started-kubernetes.html">AWS App Mesh</a></td>
<td>Open Service Mesh as an add-on</td>
<td>Yes, with <a href="https://cloud.google.com/istio/docs/istio-on-gke/migrate-to-anthos-service-mesh">Anthos Service Mesh</a></td>
</tr>
<tr class="odd">
<td><span id="NS_ClusterFirewall" class="anchor"></span>Firewall for cluster Kubernetes API</td>
<td><ul>
<li><p>CIDR allow list option</p></li>
<li><p><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Concepts/contengcidrblocks.htm">CIDR blocks and OKE</a></p></li>
</ul></td>
<td>CIDR allow list option</td>
<td>CIDR allow list option</td>
<td>CIDR allow list option</td>
</tr>
<tr class="even">
<td><span id="NS_ROrootFS" class="anchor"></span>Read-only root filesystem on node</td>
<td><a href="https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengusingpspswithoke.htm">Pod security policy required</a></td>
<td><a href="https://aws.amazon.com/blogs/opensource/using-pod-security-policies-amazon-eks-clusters/"><u>Pod security policy required</u></a></td>
<td><a href="https://docs.microsoft.com/en-us/azure/aks/policy-reference"><u>Azure policy required</u></a></td>
<td><ul>
<li><p><a href="https://cloud.google.com/kubernetes-engine/docs/concepts/node-images#file_system_layout"><u>COS: default</u></a></p></li>
<li><p><a href="https://cloud.google.com/kubernetes-engine/docs/how-to/pod-security-policies"><u>Alternative: Pod security policy required</u></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><span id="NS_SecretsManagement" class="anchor"></span>External secrets management</td>
<td><a href="https://docs.oracle.com/en-us/iaas/releasenotes/changes/6dfc3529-8e66-4cf0-8b36-ef5c696f1182/">Access OCI Vault with Secrets Store CSI Driver</a></td>
<td><a href="https://docs.aws.amazon.com/eks/latest/userguide/manage-secrets.html">AWS Secrets and Configuration Provider (ASCP) based on Secrets Store CSI Driver</a></td>
<td><a href="https://external-secrets.io/v0.5.7/provider-google-secrets-manager/">External Secrets Operator integrates with GCP Secret Manager</a></td>
<td><a href="https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-driver">Azure Key Vault Provider for Secrets Store CSI Driver</a></td>
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

#### [Supported K8s Versions][Supported Kubernetes Version(s)]
- <span id="Note_GI_K8s_Versions" class="anchor"></span>**(note 1)** Kubernetes releases happen approximately three times per year and the typical patch cadence is monthly (though not uncommon to be every 1 to 2 weeks). The best way to determine exactly which versions are currently supported on a particular platform is to utilize the Command Line Interface (CLI) of that cloud provider. Example commands are as follows:

    - **Oracle**

            oci ce cluster-options get --cluster-option-id all --query 'data."kubernetes-versions"'

    - **Azure**

            az aks get-versions --location eastus --query 'orchestrators[*].[orchestratorVersion,upgrades[*].orchestratorVersion]' --output table

    - **AWS**

            aws eks describe-addon-versions --query 'addons[0].addonVersions[0].compatibilities[*].clusterVersion'

    - **GCP** (Channel can be REGULAR, STABLE, or RAPID)

            gcloud container get-server-config --region us-east1 --flatten="channels" --filter="channels.channel=REGULAR" --format="yaml(channels.channel,channels.validVersions)"

#### [Node OS]

-   <span id="Note_GI_NodeOS_01" class="anchor"></span>**(note 1)** some, but not all, of the latest Oracle Linux images provided by Oracle Cloud Infrastructure

    - **i.e.:** “Docker is not included in Oracle Linux 8 images. Instead, in node pools running Kubernetes 1.20.x and later, Container Engine for Kubernetes installs and uses the CRI-O container runtime and the crictl CLI (for more information, see Notes about Container Engine for Kubernetes Support for Kubernetes Version 1.20).”

-   <span id="Note_GI_NodeOS_02" class="anchor"></span>**(note 2)** OKE images are provided by Oracle and built on top of platform images. OKE images are optimized for use as worker node base images, with all the necessary configurations and required software

-   **(note 3)** Custom images are provided by you and can be based on both supported platform images and OKE images. Custom images contain Oracle Linux operating systems, along with other customizations, configuration, and software that were present when you created the image.

### Service Limits

### Networking and Security

#### [RBAC][Kubernetes RBAC]

-   <span id="Note_NS_RBAC_01" class="anchor"></span>**(note 1)** “**By default, users are not assigned any Kubernetes RBAC roles (or clusterroles).** Before attempting to create a new role (or clusterrole), you must be assigned an appropriately privileged role (or clusterrole). A number of such roles and clusterroles are always created by default, including the cluster-admin clusterrole (for a full list, see Default Roles and Role Bindings in the Kubernetes documentation). The cluster-admin clusterrole essentially confers super-user privileges. A user granted the cluster-admin clusterrole can perform any operation across all namespaces in a given cluster.” ([source][RBAC_source1])

-   <span id="Note_NS_RBAC_02" class="anchor"></span>**(note 2)** “For most operations on Kubernetes clusters created and managed by Container Engine for Kubernetes, **Oracle Cloud Infrastructure Identity and Access Management (IAM)** provides access control.” ([source][RBAC_source1])

-   <span id="Note_NS_RBAC_03" class="anchor"></span>**(note 3)** “In addition to IAM, the Kubernetes RBAC Authorizer can enforce additional fine-grained access control for users on specific clusters via Kubernetes RBAC roles and clusterroles.” ([source][RBAC_source1])

#### [Pod Security][Pod Security Admission Controller]

-   <span id="NS_PodSecurityAdmissionController" class="anchor"></span>**(note 1) Kubernetes Pod Security Policy will be deprecated starting with Kubernetes version 1.21, and will be removed entirely in version 1.25.** Recommended best practice is to migrate pod security policy to pod security admission controller before the deprecation deadline.

#### [Private or public IP Address for Clusters][Private or public IP address for cluster Kubernetes API]

-   <span id="Note_NS_IPforCluster" class="anchor"></span>**(note 1)** “You access the Kubernetes API on the cluster control plane through an endpoint hosted in a subnet of your VCN. This Kubernetes API endpoint subnet can be a private or public subnet. If you specify a public subnet for the Kubernetes API endpoint, you can optionally assign a public IP address to the Kubernetes API endpoint (in addition to the private IP address). You control access to the Kubernetes API endpoint subnet using security rules defined for security lists or network security groups.”

### Container Image Services

#### [Image scanning service][]

-   <span id="Note_CIS_ImageScanningService_01" class="anchor"></span>**(note 1)** “Create and manage container image targets and to assign them to container image scan recipes. A container image target is a collection of repositories in [Container Registry] that you want scanned for security vulnerabilities.”

## **References**

- ([Oracle Developers Community]) Your one-stop shop for all Oracle Cloud Developer knowledge.

- ([StackRox]) EKS vs GKE vs AKS - Evaluating Kubernetes in the Cloud

-   ([itoutposts]) Kubernetes Engines Compared: Full Guide

-   ([veritis]) EKS Vs. AKS Vs. GKE: Which is the right Kubernetes platform for you?

-   ([kloia]) Comparison of Kubernetes Engines

  [reach us any time on Slack!]: https://bit.ly/odevrel_slack
  [Supported Kubernetes version(s)]: #GI_CurrentKs8Version
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
  [Preemptible capacity]: #GI_Preemptible_capacity
  [Cluster_Addons]: #GI_Cluster_Addons
  [Max clusters]: #SL_MaxClusters
  [Max nodes per cluster]: #SL_MaxNodesCluster
  [Max nodes per node pool/group]: #SL_MaxNodesNodePool
  [Max node pools/groups per cluster]: #SL_MaxNodePoolsCluster
  [Max pods/node]: #SL_MaxPodsNode
  [Network plugin/CNI]: #NS_NetworkPlugin
  [Workload Identity]: #NS_WorkloadIdentity
  [Kubernetes RBAC]: #NS_RBAC
  [Network policy]: #NS_NetworkPolicy
  [Pod Security Admission Controller]: #NS_PodSecurityPolicy
  [Private or public IP address for cluster Kubernetes API]: #NS_IPforCluster
  [Private or Public IP addresses for nodes]: #NS_IPforNodes
  [Pod-to-pod traffic encryption supported by provider]: #NS_EncryptedPodTraffic
  [Firewall for cluster Kubernetes API]: #NS_ClusterFirewall
  [Read-only root filesystem on node]: #NS_ROrootFS
  [External secrets management]: #NS_SecretsManagement
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
  [Oracle Developers Community]: https://developer.oracle.com/index.html
