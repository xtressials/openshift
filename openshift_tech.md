---

copyright:
  years: 2014, 2020
lastupdated: "2020-11-04"

keywords: openshift, roks, rhoks, rhos, compliance, security standards, red hat openshift, openshift container platform, red hat, openshift architecture, red hat architecture, openshift dependencies,

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}



# Service architecture and dependencies
{: #service-arch}

Review sample architectures, components, and dependencies for your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

## Classic cluster service architecture
{: #service-architecture}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> The following architectural overviews are specific to the classic infrastructure provider. For an architectural overview for the VPC infrastructure provider, see [VPC cluster service architecture](#service-architecture_vpc).
{: note}


In {{site.data.keyword.openshiftlong_notm}}, your clusters comprise an IBM-managed master that secures components such as the API server and etcd, and customer-managed worker nodes that you configure to run you app workloads, as well as {{site.data.keyword.openshiftshort}}-provided default components. The default components within the cluster, such as the {{site.data.keyword.openshiftshort}} web console or OperatorHub, vary with the {{site.data.keyword.openshiftshort}} version of your cluster.
{: shortdesc}

### {{site.data.keyword.openshiftshort}} version 4 architecture
{: #service-architecture-4}

<img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> Review the architecture diagram and then scroll through the following tables for a description of master and worker node components in {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 on classic infrastructure. For more information about the OpenShift Container Platform architecture, see the [{{site.data.keyword.openshiftshort}} docs](https://docs.openshift.com/container-platform/4.3/architecture/architecture.html){: external}.
{: shortdesc}

When you run `oc get nodes`, you might notice that the **ROLES** of your worker nodes are marked as both `master,worker`. These nodes are worker nodes in {{site.data.keyword.cloud_notm}}, and do not include the master components that are managed by IBM. Instead, these nodes are marked as `master` because they run OpenShift Container Platform components that are required to set up and manage default resources within the cluster, such as the OperatorHub and internal registry.
{: note}

![{{site.data.keyword.openshiftlong_notm}} cluster architecture](/images/cs_org_ov_both_ses_roks4.png)

#### {{site.data.keyword.openshiftshort}} version 4 master components
{: #service-architecture-4-master}

Review the following components in the IBM-managed master of your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

You cannot modify these components. IBM manages the components and automatically updates them during master patch updates.

In OpenShift Container Platform 4, many components are configured by a corresponding operator for ease of management. The following table discusses these operators and components together, to focus on the main functionality the component provides to the cluster.

| Master components| Description |
|:-----------------|:-----------------|
| Single tenancy | The master and all master components are dedicated only to you, and are not shared with other IBM customers. |
| Replicas | Master components, including the {{site.data.keyword.openshiftshort}} API server and etcd data store have three replicas and, if located in a multizone metro, are spread across zones for even higher availability. The master components are backed up every 8 hours.|
| `cloud-controller-manager` | The cloud controller manager manages cloud provider-specific components such as the {{site.data.keyword.cloud_notm}} load balancer.|
| `cluster-health` | The cluster health component monitors the health of the cluster and integrates with {{site.data.keyword.cloud_notm}} monitoring and metrics for the service.|
|  `cluster-policy-controller` | The [`cluster-policy-controller`](https://github.com/openshift/cluster-policy-controller){: external} maintains policy resources that are required to create pods within the cluster. |
| `cluster-version-operator` | The cluster version operator (CVO) installs and updates other operators that run in the cluster. For more information, see the [GitHub project](https://github.com/openshift/cluster-version-operator){: external}.|
| `control-plane-operator` | The control plane operator manages the installation and update of control plane components in the master.|
| `etcd`, `etcd-molecule`, `etcd-operator` | etcd is a highly available key value store that stores the state of all Kubernetes resources of a cluster, such as services, deployments, and pods. Data in etcd is backed up every 8 hours to an encrypted storage instance that IBM manages.|
| `kube-controller-manager`, `openshift-controller-manager` | The [Kubernetes controller](https://github.com/openshift/cluster-kube-controller-manager-operator){: external} watches the state of objects within the cluster, such as the replica set of a workload. When the state of an object changes, for example if a pod in a replica set goes down, the controller manager initiates correcting actions to achieve the required state.  The {{site.data.keyword.openshiftshort}} controller performs the same function for objects that are specific to the {{site.data.keyword.openshiftshort}} API, such as projects. |
| `kube-scheduler` | The [Kubernetes scheduler](https://github.com/openshift/cluster-kube-scheduler-operator){: external} watches for newly created pods and decides where to deploy them based on capacity, performance needs, policy constraints, anti-affinity specifications, and workload requirements. If no worker node can be found that matches the requirements, the pod is not deployed in the cluster. |
| `manifests-bootstrapper` | The manifests bootstrapper job sets up the master with the required certificates to join as the master node of the cluster. |
| `oauth-openshift` | The built-in OAuth server is automatically set up to integrate with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). You cannot add other supported identity providers to the cluster. For more information about how to authenticate with the cluster via IAM, see [Accessing {{site.data.keyword.openshiftshort}} clusters](/docs/openshift?topic=openshift-access_cluster). |
| `openshift-apiserver`, `openshift-apiserver-operator`, `kube-apiserver` | The API server is the main entry point for all cluster management requests from the worker node to the master. The API server validates and processes requests that change the state of Kubernetes objects, such as pods or services, and {{site.data.keyword.openshiftshort}} objects, such as projects or users. Then, the API server stores this state in the etcd data store.|
| `openvpnserver`, `openvpn-operator` | The OpenVPN server works with the OpenVPN client to securely connect the master to the worker node. This connection supports `apiserver proxy` calls to your pods and services; `oc exec`, `attach`, and `logs` calls to the kubelet; and mutating and validating webhooks.|
| Admission controllers | Admission controllers are implemented for specific features in {{site.data.keyword.openshiftlong_notm}} clusters. With admission controllers, you can set up policies in your cluster that determine whether a particular action in the cluster is allowed or not. In the policy, you can specify conditions when a user cannot perform an action, even if this action is part of the general permissions that you assigned the user by using RBAC. Therefore, admission controllers can provide an extra layer of security for your cluster before an API request is processed by the {{site.data.keyword.openshiftshort}} API server. </br></br> When you create an {{site.data.keyword.openshiftshort}} cluster, the following [Kubernetes admission controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/){: external} are automatically installed in the given order in the {{site.data.keyword.openshiftshort}} master, which cannot be changed by the user:<ul><li>`NamespaceLifecycle`</li><li>`LimitRanger`</li><li>`ServiceAccount`</li><li>`DefaultStorageClass`</li><li>`ResourceQuota`</li><li>`StorageObjectInUseProtection`</li><li>`PersistentVolumeClaimResize`</li><li>[`Priority`](/docs/openshift?topic=openshift-pod_priority)</li><li>`BuildByStrategy`</li><li>`OriginPodNodeEnvironment`</li><li>`PodNodeSelector`</li><li>`ExternalIPRanger`</li><li>`NodeRestriction`</li><li>`SecurityContextConstraint`</li><li>`SCCExecRestrictions`</li><li>`PersistentVolumeLabel`</li><li>`OwnerReferencesPermissionEnforcement`</li><li>`PodTolerationRestriction`</li><li>`openshift.io/JenkinsBootstrapper`</li><li>`openshift.io/BuildConfigSecretInjector`</li><li>`openshift.io/ImageLimitRange`</li><li>`openshift.io/RestrictedEndpointsAdmission`</li><li>`openshift.io/ImagePolicy`</li><li>`openshift.io/IngressAdmission`</li><li>`openshift.io/ClusterResourceQuota`</li><li>`MutatingAdmissionWebhook`</li><li>`ValidatingAdmissionWebhook`</li></ul></br><p>You can [install your own admission controllers in the cluster](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks){: external} or choose from the optional admission controllers that {{site.data.keyword.openshiftlong_notm}} provides.</p><ul><li><strong>[Container image security enforcer](/docs/Registry?topic=Registry-security_enforce#security_enforce):</strong> Use this admission controller to enforce Vulnerability Advisor policies in your cluster to block deployments from vulnerable images.</li></ul></br><p class="note">If you manually installed admission controllers and you do not want to use them anymore, make sure to remove them entirely. If admission controllers are not entirely removed, they might block all actions that you want to perform on the cluster.</p>
{: summary="The rows are read from left to right. The first column is the master component. The second column is a description of the component."}
{: caption="{{site.data.keyword.openshiftshort}} 4 master components." caption-side="top"}

#### {{site.data.keyword.openshiftshort}} version 4 worker node components
{: #service-architecture-4-workers}

Review the following components in the customer-managed worker nodes of your {{site.data.keyword.openshiftlong_notm}} cluster.
{: shortdesc}

These components run on your worker nodes because you are able to use them with the workloads that you deploy to your cluster. For example, your apps might use an operator from the OperatorHub that runs a container from an image that is stored in the internal registry. You are responsible for your usage of these components, but IBM provides updates for them in the worker node patch updates that you choose to apply.

In OpenShift Container Platform 4, many components are configured by a corresponding operator for ease of management. The following table discusses these operators and components together, to focus on the main functionality the component provides to the cluster.

| Worker node components| Description |
|:-----------------|:-----------------|
| Single tenancy | The worker nodes and all worker node components are dedicated only to you, and are not shared with other IBM customers. However, if you use worker node virtual machines, the underlying hardware might be shared with other IBM customers depending on the [level of hardware isolation](/docs/openshift?topic=openshift-planning_worker_nodes#vm) that you choose. |
| Operating System | {{site.data.keyword.openshiftlong_notm}} worker nodes run on the Red Hat Enterprise Linux 7 operating system. |
| Projects | {{site.data.keyword.openshiftshort}} organizes your resources into projects, which are Kubernetes namespaces with annotations, and includes many more components than community Kubernetes clusters to run {{site.data.keyword.openshiftshort}} features such as the catalog. Select components of projects are described in the following rows. For more information, see [Working with projects](http://docs.openshift.com/container-platform/4.3/applications/projects/working-with-projects.html){: external}.|
| `calico-system`, `tigera-operator` | Calico manages network policies for your cluster, and includes a few components to manage container network connectivity, IP address assignment, and network traffic control. The Tigera operator installs and manages the lifecycle of Calico components.|
| `default` | This project is used if you do not specify a project or create a project for your Kubernetes resources.|
| `ibm-system` | This project includes the `ibm-cloud-provider-ip` deployment that works with `keepalived` to provide health checking and Layer 4 load balancing for requests to app pods.|
| `kube-system` | This project includes many components that are used to run Kubernetes on the worker node.<ul><li>**`ibm-master-proxy`**: The `ibm-master-proxy` is a daemon set that forwards requests from the worker node to the IP addresses of the highly available master replicas. In single zone clusters, the master has three replicas on separate hosts. For clusters that are in a multizone-capable zone, the master has three replicas that are spread across zones. A highly available load balancer forwards requests to the master domain name to the master replicas.</li><li>**`kubelet`**: The kubelet is a worker node agent that runs on every worker node and is responsible for monitoring the health of pods that run on the worker node and for watching the events that the API server sends. Based on the events, the kubelet creates or removes pods, ensures liveness and readiness probes, and reports back the status of the pods to the API server.</li><li>**`vpn`**: The OpenVPN client works with the OpenVPN server to securely connect the master to the worker node. This connection supports `apiserver proxy` calls to your pods and services, and `oc exec`, `attach`, and `logs` calls to the kubelet.</li><li>**Other components**: The `kube-system` project also includes components to manage IBM-provided resources such as storage plug-ins for file and block storage, ingress application load balancer (ALB), and `keepalived`.</li></ul>|
| `openshift-cloud-credential-operator` | The cloud credential operator manages a controller for {{site.data.keyword.openshiftshort}} components that request cloud provider credentials. The controller ensures that only the credentials that are required for the operation are used, and not any elevated permissions like `admin`. For more information, see the [GitHub project](https://github.com/openshift/cloud-credential-operator){: external}.|
| `openshift-cluster-node-tuning-operator` | IBM manages the [node tuning operator](https://docs.openshift.com/container-platform/4.3/scalability_and_performance/using-node-tuning-operator.html){: external}, which runs a daemon set on each worker node in the cluster to tune the default worker node settings. You cannot edit the default worker node settings. |
| `openshift-cluster-samples-operator` | The [samples operator](https://docs.openshift.com/container-platform/4.3/openshift_images/configuring-samples-operator.html){: external} manages select image streams and templates that come with the {{site.data.keyword.openshiftshort}} cluster by default. You can deploy these templates from the [**Developer** perspective in the {{site.data.keyword.openshiftshort}} web console](/docs/openshift?topic=openshift-deploy_app#openshift_console). |
| `openshift-cluster-storage-operator` | The cluster storage operator makes sure that a default storage class is set. To review or change the default {{site.data.keyword.cloud_notm}} storage class, see [Changing the default storage class](/docs/openshift?topic=openshift-kube_concepts#default_storageclass). |
| `openshift-console`, `openshift-console-operator` | The {{site.data.keyword.openshiftshort}} web console is a user-friendly, web-based interface that you can use to manage the {{site.data.keyword.openshiftshort}} and Kubernetes resources that run in your cluster. You can also use the console to display an `oc login` token to authenticate to your cluster from a CLI. For more information, see [Navigating the {{site.data.keyword.openshiftshort}} console](/docs/openshift?topic=openshift-openshift_tutorial#openshift_oc_console).|
| `openshift-dns`, `openshift-dns-operator` | The DNS project includes the components to validate incoming network traffic against the `iptables` rules that are set up on the worker node, and proxies requests that are allowed to enter or leave the cluster.|
| `openshift-image-registry` | {{site.data.keyword.openshiftshort}} provides an internal [container image registry](https://docs.openshift.com/container-platform/4.3/registry/architecture-component-imageregistry.html){: external} that you can use to locally manage and view images through the console. Alternatively, you can [set up the private {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-registry#openshift_iccr) or [import images from {{site.data.keyword.registrylong_notm}} to the internal registry](/docs/openshift?topic=openshift-registry#imagestream_registry). The internal registry comes with a classic {{site.data.keyword.cloud_notm}} File Storage volume in your IBM Cloud infrastructure account to [store the registry images](/docs/openshift?topic=openshift-registry#openshift_internal_registry). The file storage volume is provisioned through the `image-registry-storage` persistent volume claim (PVC).|
| `openshift-ingress`, `openshift-ingress-operator` | {{site.data.keyword.openshiftshort}} uses [routes](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html){: external} to directly expose an app's service on a hostname so that external clients can reach the service. To create routes, the cluster uses the Ingress operator.</br></br>You can also use [Ingress](/docs/openshift?topic=openshift-ingress-about-roks4) to expose apps externally and customize routing. Ingress consists of three components: the Ingress controller, router, and Ingress resources. The router maps the service to the hostname. By default, the router includes two replicas. Make sure that your cluster has at least two worker nodes so that the router can run on separate compute hosts for higher availability.|
| `openshift-marketplace` | The marketplace includes the [OperatorHub](https://docs.openshift.com/container-platform/4.3/operators/olm-understanding-operatorhub.html){: external} that comes with the {{site.data.keyword.openshiftshort}} cluster by default. The OperatorHub includes operators from Red Hat and 3rd-party providers. Keep in mind that these operators are provided by the community, might not integrate with your cluster, and are not supported by IBM. You can [enable operators](/docs/openshift?topic=openshift-operators) from the OperatorHub in {{site.data.keyword.openshiftshort}} web console. |
| `openshift-monitoring` | OpenShift Container Platform includes a [built-in monitoring stack](http://docs.openshift.com/container-platform/4.3/monitoring/cluster_monitoring/about-cluster-monitoring.html){: external} for your cluster, that includes metrics and alert managing capabilities. For a comparison of the built-in monitoring stack and other options such as {{site.data.keyword.mon_full_notm}}, see [Understanding options for logging and monitoring](/docs/openshift?topic=openshift-health). |
| `openshift-multus` | OpenShift Container Platform uses the Multus container network interface (CNI) plug-in to allow [multiple pod networks](https://docs.openshift.com/container-platform/4.3/networking/multiple_networks/understanding-multiple-networks.html){: external}. However, you cannot configure the cluster to use multiple pod networks. {{site.data.keyword.openshiftlong_notm}} clusters support only Calico, which is set up for your cluster by default. If enabled, [Service Mesh](https://docs.openshift.com/container-platform/4.3/service_mesh/v1x/servicemesh-release-notes.html){: external} uses the Multus plug-in. |
| `openshift-network-operator` | The [cluster network operator (CNO)](https://docs.openshift.com/container-platform/4.3/networking/cluster-network-operator.html){: external} manages the cluster network components that are set up by default, such as the CNI pod network provider plug-in and DNS operator.|
| `openshift-operator-lifecycle-manager` | The [operator lifecycle manager (OLM)](https://docs.openshift.com/container-platform/4.3/operators/understanding_olm/olm-understanding-olm.html){: external} manages the lifecycle of all operators and the catalog that run in the cluster, including the operators for the default components and any custom operators that you add.|
| `openshift-service-ca`, `openshift-service-ca-operator` | The certificate authority (CA) operator runs certificate signing and injects certificates into API server resources and configmaps in the cluster. For more information, see the [GitHub project](https://github.com/openshift/service-ca-operator){: external}.|
{: summary="The rows are read from left to right. The first column is the worker node component. The second column is a description of the component."}
{: caption="{{site.data.keyword.openshiftshort}} 4 worker node components." caption-side="top"}

### {{site.data.keyword.openshiftshort}} version 3 architecture
{: #service-architecture-3}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> Review the architecture diagram and then scroll through the following table for a description of master and worker node components in {{site.data.keyword.openshiftlong_notm}} clusters that run version 3. For more information about the OpenShift Container Platform architecture, see the [{{site.data.keyword.openshiftshort}} docs](https://docs.openshift.com/container-platform/3.11/architecture/index.html){: external}.
{: shortdesc}

![{{site.data.keyword.openshiftlong_notm}} cluster architecture](/images/cs_org_ov_both_ses_roks.png)

| Master components| Description |
|:-----------------|:-----------------|
| Single tenancy | The master and all master components are dedicated only to you, and are not shared with other IBM customers. |
| Replicas | Master components, including the {{site.data.keyword.openshiftshort}} Kubernetes API server and etcd data store have three replicas and, if located in a multizone metro, are spread across zones for even higher availability. The master components are backed up every 8 hours.|
| `openshift-api` | The {{site.data.keyword.openshiftshort}} Kubernetes API server serves as the main entry point for all cluster management requests from the worker node to the master. The API server validates and processes requests that change the state of Kubernetes resources, such as pods or services, and stores this state in the etcd data store.|
| `openvpn-server` | The OpenVPN server works with the OpenVPN client to securely connect the master to the worker node. This connection supports `apiserver proxy` calls to your pods and services, and `oc exec`, `attach`, and `logs` calls to the kubelet.|
| `etcd` | etcd is a highly available key value store that stores the state of all Kubernetes resources of a cluster, such as services, deployments, and pods. Data in etcd is backed up to an encrypted storage instance that IBM manages.|
| `openshift-controller` | The {{site.data.keyword.openshiftshort}} controller manager watches for newly created pods and decides where to deploy them based on capacity, performance needs, policy constraints, anti-affinity specifications, and workload requirements. If no worker node can be found that matches the requirements, the pod is not deployed in the cluster. The controller also watches the state of cluster resources, such as replica sets. When the state of a resource changes, for example if a pod in a replica set goes down, the controller manager initiates correcting actions to achieve the required state. The `openshift-controller` functions as both the scheduler and controller manager in a community Kubernetes configuration. |
| `cloud-controller-manager` | The cloud controller manager manages cloud provider-specific components such as the {{site.data.keyword.cloud_notm}} load balancer.|
| Admission controllers | Admission controllers are implemented for specific features in {{site.data.keyword.openshiftlong_notm}} clusters. With admission controllers, you can set up policies in your cluster that determine whether a particular action in the cluster is allowed or not. In the policy, you can specify conditions when a user cannot perform an action, even if this action is part of the general permissions that you assigned the user by using RBAC. Therefore, admission controllers can provide an extra layer of security for your cluster before an API request is processed by the API server. </br></br> When you create an {{site.data.keyword.openshiftshort}} cluster, the following [Kubernetes admission controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/){: external} are automatically installed in the given order in the {{site.data.keyword.openshiftshort}} master, which cannot be changed by the user:<ul><li>`NamespaceLifecycle`</li><li>`LimitRanger`</li><li>`ServiceAccount`</li><li>`DefaultStorageClass`</li><li>`ResourceQuota`</li><li>`StorageObjectInUseProtection`</li><li>`PersistentVolumeClaimResize`</li><li>[`Priority`](/docs/openshift?topic=openshift-pod_priority)</li><li>`BuildByStrategy`</li><li>`OriginPodNodeEnvironment`</li><li>`PodNodeSelector`</li><li>`ExternalIPRanger`</li><li>`NodeRestriction`</li><li>`SecurityContextConstraint`</li><li>`SCCExecRestrictions`</li><li>`PersistentVolumeLabel`</li><li>`OwnerReferencesPermissionEnforcement`</li><li>`PodTolerationRestriction`</li><li>`openshift.io/JenkinsBootstrapper`</li><li>`openshift.io/BuildConfigSecretInjector`</li><li>`openshift.io/ImageLimitRange`</li><li>`openshift.io/RestrictedEndpointsAdmission`</li><li>`openshift.io/ImagePolicy`</li><li>`openshift.io/IngressAdmission`</li><li>`openshift.io/ClusterResourceQuota`</li><li>`MutatingAdmissionWebhook`</li><li>`ValidatingAdmissionWebhook`</li></ul></br><p>You can [install your own admission controllers in the cluster](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks){: external} or choose from the optional admission controllers that {{site.data.keyword.openshiftlong_notm}} provides.</p><ul><li><strong>[Container image security enforcer](/docs/Registry?topic=Registry-security_enforce#security_enforce):</strong> Use this admission controller to enforce Vulnerability Advisor policies in your cluster to block deployments from vulnerable images.</li></ul></br><p class="note">If you manually installed admission controllers and you do not want to use them anymore, make sure to remove them entirely. If admission controllers are not entirely removed, they might block all actions that you want to perform on the cluster.</p>
{: caption="{{site.data.keyword.openshiftshort}} 3 master components." caption-side="top"}
{: #roks-components-1}
{: tab-title="Master"}
{: tab-group="roks-components"}
{: class="simple-tab-table"}

| Worker node components| Description |
|:-----------------|:-----------------|
| Single tenancy | The worker nodes and all worker node components are dedicated only to you, and are not shared with other IBM customers. However, if you use worker node virtual machines, the underlying hardware might be shared with other IBM customers depending on the [level of hardware isolation](/docs/openshift?topic=openshift-planning_worker_nodes#vm) that you choose. |
| Operating System | {{site.data.keyword.openshiftlong_notm}} worker nodes run on the Red Hat Enterprise Linux 7 operating system. |
| Projects | {{site.data.keyword.openshiftshort}} organizes your resources into projects, which are Kubernetes namespaces with annotations, and includes many more components than community Kubernetes clusters to run {{site.data.keyword.openshiftshort}} features such as the catalog. Select components of projects are described in the following rows. For more information, see [Working with projects](http://docs.openshift.com/container-platform/4.3/applications/projects/working-with-projects.html){: external}.|
| `kube-system` | This namespace includes many components that are used to run Kubernetes on the worker node.<ul><li>**`ibm-master-proxy`**: The `ibm-master-proxy` is a daemon set that forwards requests from the worker node to the IP addresses of the highly available master replicas. In single zone clusters, the master has three replicas on separate hosts. For clusters that are in a multizone-capable zone, the master has three replicas that are spread across zones. A highly available load balancer forwards requests to the master domain name to the master replicas.</li><li>**`openvpn-client`**: The OpenVPN client works with the OpenVPN server to securely connect the master to the worker node. This connection supports `apiserver proxy` calls to your pods and services, and `oc exec`, `attach`, and `logs` calls to the kubelet.</li><li>**`kubelet`**: The kubelet is a worker node agent that runs on every worker node and is responsible for monitoring the health of pods that run on the worker node and for watching the events that the Kubernetes API server sends. Based on the events, the kubelet creates or removes pods, ensures liveness and readiness probes, and reports back the status of the pods to the Kubernetes API server.</li><li>**`calico`**: Calico manages network policies for your cluster, and includes a few components to manage container network connectivity, IP address assignment, and network traffic control.</li><li>**Other components**: The `kube-system` namespace also includes components to manage IBM-provided resources such as storage plug-ins for file and block storage, ingress application load balancer (ALB), `fluentd` logging, and `keepalived`.</li></ul>|
| `ibm-system` | This namespace includes the `ibm-cloud-provider-ip` deployment that works with `keepalived` to provide health checking and Layer 4 load balancing for requests to app pods.|
| `kube-proxy-and-dns`| This namespace includes the components to validate incoming network traffic against the `iptables` rules that are set up on the worker node, and proxies requests that are allowed to enter or leave the cluster.|
| `default` | This namespace is used if you do not specify a namespace or create a project for your Kubernetes resources. In addition, the default namespace includes the following components to support your {{site.data.keyword.openshiftshort}} clusters.<ul><li>**`router`**: {{site.data.keyword.openshiftshort}} uses [routes](https://docs.openshift.com/container-platform/3.11/dev_guide/routes.html){: external} to expose an app's service on a hostname so that external clients can reach the service. The router maps the service to the hostname. By default, the router includes two replicas. Make sure that your cluster has at least two worker nodes so that the router can run on separate compute hosts for higher availability.</li><li>**`docker-registry`** and **`registry-console`.**: {{site.data.keyword.openshiftshort}} provides an internal [container image registry](https://docs.openshift.com/container-platform/3.11/install_config/registry/index.html){: external} that you can use to locally manage and view images through the console. Alternatively, you can set up the private {{site.data.keyword.registrylong_notm}}. The internal registry comes with a classic {{site.data.keyword.cloud_notm}} File Storage volume in your IBM Cloud infrastructure account to [store the registry images](/docs/openshift?topic=openshift-registry#openshift_internal_registry) that is provisioned through the `registry-backing` persistent volume claim (PVC).</li></ul>|
| Other projects | Other components are installed in various namespaces by default to enable functionality such as logging, monitoring, and the {{site.data.keyword.openshiftshort}} console.<ul><li><code>ibm-cert-store</code></li><li><code>kube-public</code></li><li><code>kube-service-catalog</code></li><li><code>openshift</code></li><li><code>openshift-ansible-service-broker</code></li><li><code>openshift-console</code></li><li><code>openshift-infra</code></li><li><code>openshift-monitoring</code></li><li><code>openshift-node</code></li><li><code>openshift-template-service-broker</code></li><li><code>openshift-web-console</code></li></ul>|
{: caption="{{site.data.keyword.openshiftshort}} 3 worker node components." caption-side="top"}
{: #roks-components-2}
{: tab-title="Worker nodes"}
{: tab-group="roks-components"}
{: class="simple-tab-table"}

<br />



## VPC cluster service architecture
{: #service-architecture_vpc}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> The following architectural overviews are specific to the VPC infrastructure provider, which is available for clusters that run version 4 only. For an architectural overview for the classic infrastructure provider, see [Classic cluster service architecture](#service-architecture).
{: note}

Review the architecture diagrams and then scroll through the following table for a description of master and worker node components in {{site.data.keyword.openshiftlong_notm}} clusters that run version 4 on virtual private cloud (VPC) compute infrastructure.
{: shortdesc}

**Cluster with public and private service endpoints**:

The following diagram shows the components of your cluster and how they interact when both the [public and private service endpoints are enabled](/docs/openshift?topic=openshift-plan_clusters#vpc-workeruser-master). Because both service endpoints are enabled, your VPC creates a public load balancer for each service for inbound traffic.

<p>
<figure>
 <img src="/images/arch_roks_vpc.png" alt="{{site.data.keyword.openshiftlong_notm}} on VPC cluster architecture with public and private service endpoints">
 <figcaption>{{site.data.keyword.openshiftlong_notm}} on VPC cluster architecture when public and private public service endpoints are enabled</figcaption>
</figure>
</p>

**Cluster with private service endpoint only**:

The following diagram shows the components of your cluster and how they interact when only the [private service endpoint is enabled](/docs/openshift?topic=openshift-plan_clusters#vpc-workeruser-master). Because only the private service endpoint is enabled, your VPC creates a private load balancer for each service for inbound traffic.

<p>
<figure>
 <img src="/images/arch_roks_vpc_private.png" alt="{{site.data.keyword.openshiftlong_notm}} on VPC cluster architecture with the private service endpoint only">
 <figcaption>{{site.data.keyword.openshiftlong_notm}} on VPC cluster architecture when only the private public service endpoint is enabled</figcaption>
</figure>
</p>

[Masters](#service-architecture-4-master) and [worker nodes](#service-architecture-4-workers) include the same components as described in the Classic cluster architecture for version 4 clusters. For more information about the OpenShift Container Platform architecture, see the [{{site.data.keyword.openshiftshort}} docs](https://docs.openshift.com/container-platform/4.3/architecture/architecture.html){: external}.

| Component | Description |
|:-----------------|:-----------------|
| Master | [Master components](#service-architecture-4-master), including the API server and etcd, have three replicas and are spread across zones for even higher availability. Masters include the same components as described in the Classic cluster architecture for version 4 clusters. The master and all the master components are dedicated only to you, and are not shared with other IBM customers. |
| Worker node | With {{site.data.keyword.openshiftlong_notm}}, the virtual machines that your cluster manages are instances that are called worker nodes. These worker nodes virtual machines and all the worker node components are dedicated to you only and are not shared with other IBM customers. However, the underlying hardware is shared with other IBM customers. For more information, see [Virtual machines](/docs/openshift?topic=openshift-planning_worker_nodes#vm). </br></br> You manage the worker nodes through the automation tools that are provided by {{site.data.keyword.openshiftlong_notm}}, such as the API, CLI, or console. Unlike classic clusters, you do not see VPC compute worker nodes in your infrastructure portal or separate infrastructure bill, but instead manage all maintenance and billing activity for the worker nodes from {{site.data.keyword.openshiftlong_notm}}.<br><br>Worker nodes include the same [components](#service-architecture-4-workers) as described in the Classic cluster architecture for version 4 clusters. {{site.data.keyword.openshiftlong_notm}} worker nodes run on the Red Hat Enterprise Linux 7 operating system.<p class="note">When you run `oc get nodes`, you might notice that the **ROLES** of your worker nodes are marked as both `master,worker`. These nodes are worker nodes in {{site.data.keyword.cloud_notm}}, and do not include the master components that are managed by IBM. Instead, these nodes are marked as `master` because they run OpenShift Container Platform components that are required to set up and manage default resources within the cluster, such as the OperatorHub and internal registry.</p> |
| Cluster networking | Your worker nodes are created in a VPC subnet in the zone that you specify. Communication between the master and worker nodes is over the private network. If you create a cluster with the public and private service endpoints enabled, authenticated external users can communicate with the master over the public network, such as to run `oc` commands. If you create a cluster with only the private service endpoints enabled, authenticated external users can communicate with the master over the private network only. You can set up your cluster to communicate with resources in on-premises networks, other VPCs, or classic infrastructure by setting up a VPC VPN, {{site.data.keyword.dl_full_notm}}, or {{site.data.keyword.tg_full_notm}} on the private network. |
| App networking | VPC load balancers are automatically created in your VPC outside the cluster for any networking services that you create in your cluster. For example, a VPC load balancer exposes the router services in your cluster by default. Or, you can create a Kubernetes `LoadBalancer` service for your apps, and a VPC load balancer is automatically generated. VPC load balancers are multizonal and route requests for your app through the private NodePorts that are automatically opened on your worker nodes. If the public and private service endpoints are enabled, the routers and VPC load balancers are created as public by default. If the only the private service endpoint is enabled, the routers and VPC load balancers are created as private by default. For more information, see [Public](/docs/openshift?topic=openshift-cs_network_planning#pattern_public_vpc) or [Private app networking for VPC clusters](/docs/openshift?topic=openshift-cs_network_planning#private_vpc).<br><br>Calico is used as the cluster networking policy fabric. |
| Storage | You can set up {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.databases-for}} only. |

<br />


## Overview of personal and sensitive data storage and removal options
{: #ibm-data}

Review what information is stored with IBM when you use {{site.data.keyword.openshiftlong_notm}}, how this data is stored and encrypted, and how you can permanently remove this information.
{: shortdesc}

### What information is stored with IBM when using {{site.data.keyword.openshiftlong_notm}}?
{: #pi-info}

For each cluster that you create with {{site.data.keyword.openshiftlong_notm}}, IBM stores the information that is described in the following table: 

|Information type|Data|
|-------|----------|
|Personal information|The email address of the {{site.data.keyword.cloud_notm}} account that created the cluster.|
|Sensitive information|<ul><li>The TLS certificate and secret that is used for the assigned Ingress subdomain. </li><li>The certificate authority that is used for the TLS certificate. </li><li>The certificate authority, private keys, and TLS certificates for the {{site.data.keyword.openshiftshort}} master components, including the {{site.data.keyword.openshiftshort}} API server, etcd data store, and VPN.</li><li>A customer root key in {{site.data.keyword.keymanagementservicelong_notm}} for each {{site.data.keyword.cloud_notm}} account that is used to encrypt personal and sensitive information.</li></ul>|


### How is my information stored and encrypted?
{: #pi-storage}

All information is stored in an etcd database and backed up every 8 hours to {{site.data.keyword.cos_full_notm}}. The etcd database and {{site.data.keyword.cos_short}} service instance are owned and managed by the {{site.data.keyword.cloud_notm}} SRE team. For each {{site.data.keyword.cloud_notm}} account, a customer root key in {{site.data.keyword.keymanagementservicelong_notm}} is created that is managed by the {{site.data.keyword.openshiftlong_notm}} service team. This root key is used to encrypt all personal and sensitive information in etcd and in {{site.data.keyword.cos_short}}.

### Where is my information stored?
{: #pi-location}

The location where your information is stored depends on the location your cluster is in. By default, your data is stored in the {{site.data.keyword.openshiftlong_notm}} multizone metro area that is closest to your cluster. However, {{site.data.keyword.openshiftlong_notm}} might decide to store your data in a different multizone metro area to optimize the utilization of available compute resources. If you create your cluster in a non-multizone metro area, your data is still stored in the closest multizone metro area. This location might be in a different country than the one where you created your cluster. Make sure that your information can reside in a different country before you create your cluster in a non-multizone metro area. 

The data that you create and own is always stored in the same location as the cluster. For more information about what data you can create in your cluster, how this data is encrypted, and how you can protect this data, see [Protecting sensitive information in your cluster](/docs/containers?topic=containers-encryption).
{: note}

### How can I remove my information?
{: #pi-removal}

Review your options to remove your information from {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

Removing personal and sensitive information is permanent and nonreversible. Make sure that you want to permanently remove your information before you proceed.
{: important}

**Is my data removed when I remove the cluster?**</br>
Deleting a cluster does not remove all information from {{site.data.keyword.openshiftlong_notm}}. When you delete a cluster, cluster-specific information is removed from the etcd instance that is managed by IBM. However, your information still exists in the {{site.data.keyword.cos_full_notm}} backup and can still be accessed by the IBM service team by using the account-specific customer root key in {{site.data.keyword.keymanagementservicelong_notm}} that IBM owns and manages. 

**What options do I have to permanently remove my data?**</br>
To remove that data that IBM stores, choose between the following options. Note that removing your personal and sensitive information requires all of your clusters to be deleted as well. Make sure that you backed up your app data before your proceed.

- **Open an {{site.data.keyword.cloud_notm}} support case**: Contact IBM Support to remove your personal and sensitive information from {{site.data.keyword.openshiftlong_notm}}. For more information, see [Getting support](/docs/get-support?topic=get-support-using-avatar).
- **End your {{site.data.keyword.cloud_notm}} subscription**: After you end your {{site.data.keyword.cloud_notm}} subscription, {{site.data.keyword.openshiftlong_notm}} removes the customer root key in {{site.data.keyword.keymanagementservicelong_notm}} that IBM created and managed for you as well as all the personal and sensitive information from the etcd data store and {{site.data.keyword.cos_short}} backup. 

### Does Red Hat collect information about my cluster?
{: #pi-rh-telemetry}

Yes. To improve the OpenShift Container Platform service, a telemetry component is installed in your cluster by default that collects anonymized health reports about your cluster. For more information, see the [{{site.data.keyword.openshiftshort}} documentation](https://docs.openshift.com/container-platform/4.5/support/remote_health_monitoring/about-remote-health-monitoring.html){: external}.

To remove the telemetry component, see [Disabling remote health reporting](/docs/openshift?topic=openshift-health#oc_disable_telemetry_reports).

## Dependencies to other {{site.data.keyword.cloud_notm}} services
{: #dependencies-ibmcloud}

Review the {{site.data.keyword.cloud_notm}} services that {{site.data.keyword.openshiftlong_notm}} connects to over the public network. 
{: shortdesc}


| Service name | Description| 
| -----------|-------------------------------| 
| Business Support Services for {{site.data.keyword.cloud_notm}} (BSS) | The `BSS` component is used to access information about the {{site.data.keyword.cloud_notm}} account, service subscription, service usage, and billing. | 
|{{site.data.keyword.cloudcerts_short}}|This service is used to retrieve the TLS certificates for custom Ingress domains that {{site.data.keyword.containerlong_notm}} users set up.|
| Global Search and Tagging (Ghost) | The `Ghost` component is used to look up information about other {{site.data.keyword.cloud_notm}} services, such as IDs, tags, or service attributes. |
| Hypersync and hyperwarp | This {{site.data.keyword.cloud_notm}} component is used to provide information about clusters so that the cluster is visible to other {{site.data.keyword.cloud_notm}} services and cluster information can be searched and displayed. |
|{{site.data.keyword.cloud_notm}} Command Line (CLI)|When {{site.data.keyword.openshiftlong_notm}} runs CLI commands, the service connects to the service API endpoint over the public service endpoint.|
|{{site.data.keyword.registrylong_notm}}|This service is used to store the container images that {{site.data.keyword.openshiftlong_notm}} uses to run the service.|
| {{site.data.keyword.la_full_notm}} | {{site.data.keyword.openshiftlong_notm}} sends service logs to {{site.data.keyword.la_full_notm}}. These logs are monitored and analyzed by the service team to detect service issues and malicious activities. You can also use {{site.data.keyword.la_full_notm}} to manage your own pod container logs. To use {{site.data.keyword.la_full_notm}}, you must deploy a logging agent to every worker node in your cluster. This agent collects pod logs from all namespaces, including `kube-system`, and forwards the logs to {{site.data.keyword.la_full_notm}}. To get started, see [Forwarding cluster and app logs to {{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-health#openshift_logdna).  |
| {{site.data.keyword.mon_full_notm}} | {{site.data.keyword.openshiftlong_notm}} sends service metrics to {{site.data.keyword.mon_full_notm}}. These metrics are monitored by the service team to identify capacity and performance issues of the service. You can also use {{site.data.keyword.mon_full_notm}} to gain operational visibility into the performance and health of your apps. For more information, see [Forwarding cluster and app metrics to {{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-health#openshift_sysdig).|
| {{site.data.keyword.cloudaccesstraillong_notm}} | {{site.data.keyword.openshiftlong_notm}} integrates with {{site.data.keyword.at_full_notm}} to forward cluster audit events to the {{site.data.keyword.at_full_notm}} service instance that is set up and owned by the {{site.data.keyword.openshiftlong_notm}} user. For more information, see [{{site.data.keyword.cloudaccesstraillong_notm}} events](/docs/containers?topic=containers-at_events).|
| IBMid profile service | The IBMid component is used to look up the IBMid from an email address. The IBMid is used to authenticate with {{site.data.keyword.cloud_notm}} via Identity and Access Management (IAM). |
| Identity and Access Management (IAM) | To authenticate requests to the service and authorize user actions, {{site.data.keyword.openshiftlong_notm}} implements platform and service access roles in Identity and Access Management (IAM). For more information about required IAM permissions to work with the service, see [Assigning cluster access](/docs/containers?topic=containers-users). |
| Infrastructure Management System (IMS) | The Infrastructure Management System (IMS) component is used to provision, manage, and show information about classic infrastructure resources of the cluster, such as worker nodes, VLANs or subnets. |
| {{site.data.keyword.keymanagementservicelong_notm}} | To protect your cluster resources and data, {{site.data.keyword.openshiftlong_notm}}. uses {{site.data.keyword.keymanagementservicelong_notm}} root keys to encrypt data in etcd, secrets, and on the worker node drive. For additional encryption, you can enable {{site.data.keyword.keymanagementserviceshort}} as a key management system provider in your cluster. For more information about how data is encrypted, see [Overview of cluster encryption](/docs/containers?topic=containers-encryption#encrypt_ov). | 
|{{site.data.keyword.cos_short}} (COS)|This service is used to store customer logs for all cluster master operations, such as `deploy`, `patch`, `update`, or `delete`, and to back up cluster metrics. Access to this service instance is protected by IAM policies and available to the {{site.data.keyword.openshiftlong_notm}} service team only to detect malicious activity. All data is encrypted in transit and at rest.|
| User Account & Authentication (UAA) | This service is used to provide OAuth authentication for Cloud Foundry services. | 

## Dependencies to 3rd party services
{: #dependencies-3rd-party}

Review the list of 3rd party services that {{site.data.keyword.openshiftlong_notm}} connects to over the public network. 
{: shortdesc}

| Service name | Description| 
| -----------|-------------------------------| 
| Akamai, Cloudflare | Akamai and Cloudflare are used as the primary providers for DNS, global load balancing, and web firewall capabilities in {{site.data.keyword.openshiftlong_notm}}. With global load balancing, these providers decrypt requests to the product API server, read the header packet of the request, and reencrypt the request before forwarding to the product API server. The header packet can include information such as the requested API method, time, or region. Note that this process applies only to requests to the product API server, and not to other requests, such as to apps in your cluster over the Ingress subdomain or custom domains. |
| GitHub Enterprise | GitHub Enterprise is used to track service enhancements, features, and customer issues. When a customer issue is identified, the cluster ID, worker node IDs, the flavor of the worker nodes, and the zone where the worker nodes are deployed to are documented. This information is then shared with the service team to start troubleshooting the issue. | 
| Launch Darkly | To manage the roll out of new features in {{site.data.keyword.openshiftlong_notm}}, Launch Darkly feature flags are used. A feature flag controls the visibility and availability of a feature to a selected user base. | 
| Let's Encrypt | This service is used as the Certificate authority to generate SSL certificates for customer owned public endpoints. All generated certificates are managed in {{site.data.keyword.cloudcerts_short}}.|
| Razee | [Razee](https://razee.io/){: external} is an open-source project that was developed by IBM to automate and manage the deployment of Kubernetes resources, versions, features, and security patches across {{site.data.keyword.openshiftlong_notm}} environments, and to visualize deployment information. Razee integrates with Launch Darkly to control the visibility of these features to the {{site.data.keyword.openshiftlong_notm}} user base. You can also use Razee to manage the rollout of your own deployments across multiple clusters. For more information, see the [Razee documentation](https://github.com/razee-io/Razee){: external}.   |
| Slack | Slack is used as the IBM-internal communication medium to troubleshoot cluster issues and bring together internal SMEs to resolve customer issues. Diagnostic information about clusters are sent to a private Slack channel and include the customer account ID, cluster ID, and details about the worker nodes. |
