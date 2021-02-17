---
# Introducing Metal³
### Kubernetes Native Bare Metal Management
---




### Why another provisioning tool?

| Self-Hosted Kubernetes Native | Hardware Management | Self-Managed  |
| :---        |    :----:   |          ---: |
| Manage your infrastructure through Kubernetes APIs using the Metal3 and machine-api CRDs. | Configure/Provision Physical resources like Servers with ease comparable to Cloud Providers | Integration with the Cluster API  from SIG Cluster-Lifecycle allows  your bare metal cluster to manage  its own growth, just like your  cloud-based clusters.  |
| Metal3 runs inside your cluster,  avoiding the need for an external  dependency.   | There are plans to include support for more hardware resources like switches, routers, etc..         |       |



### Representations of Cluster Members

| Core Kubernetes | Cluster API | Metal3  |
| :---        |    :----:   |          ---: |
| Node represents a running instance of  kubelet, its managed via Kubernetes | Machine represents a request for a place to  run kubelet, its managed by MachineDeployment | BareMetalHost represents a physical computer,  via proﬁle and inventory data. It’s managed via controller in the  baremetal-operator |
|  | Some other members include MachineSet, KubeadmControlplane, etc. | Some other members include Metal3Machine, Metal3Cluster, etc |



### Metal3 Components

<img data-src="metal3_components.png" height="80%" width="85%" />




### Metal3 Components Description

* The **baremetal-operator** is the component that manages bare metal hosts. It exposes a new BareMetalHost custom resource in the Kubernetes API that lets you manage hosts in a declarative way.
<br />
<br />
<br />
<br />
<br />
* **cluster-api-provider-metal3** is the component that provides integration with the cluster-api project. This provider includes a Metal3Machine object that acts as a client of the BareMetalHost custom resources (CR).



### Metal3 Integration with Cluster API

<img data-src="metal3_int_capi.png" height="70%" width="85%" />

[If interested, here is a link for Relational Diagram for CRs](https://github.com/metal3-io/metal3-docs/blob/master/images/v1a2_crs.png)



### Worker Deployment

| Set Up Hosts -> | Manage Inventory -> | Create Machines ->  |  Provision -> | Operations -> |
| :---        |    :----:   |     :----: | :----: | ---: |
| Connect hosts to the  provisioning network and cluster network | Collect IPMI/iDrac/supported-protocol credentials and MAC  addresses for hosts on  the provisioning  network. | Create Machine CRs  (either individually or  by scaling a  MachineSet) | The Bare Metal  Operator uses Ironic  hosted on the cluster  to install an image on  the worker hosts. | Nodes join the cluster. |
|  | Create BareMetalHost(BMH)  CRs in the cluster that  reﬂect available nodes | Machine manages Metal3Machine which picks a suitable BMH to provision | Config data is passed as part of deployment. | Ironic monitors power  state and host health. |
|  |  | Machine CR also references the Kubeadmconfig for the node | Control Plane is provisioned before Workers |  |



### Sample Bare Metal Host CR

```
apiVersion: metal3.io/v1alpha1
kind: BareMetalHost
metadata:
  name: bm0
spec:
  online: true
  bmc:
    address: idrac://192.168.122.1:6230/
    credentialsName: bm0-bmc-secret
  bootMACAddress: 52:54:00:b7:b2
```



### Resources

#### [Metal3 Website](https://metal3.io)

#### [Metal3 GitHub Project Page](https://github.com/metal3-io)

#### [Cluster API Website](https://cluster-api.sigs.k8s.io/)

#### [Cluster API GitHub](https://github.com/kubernetes-sigs/cluster-api)

#### [Ironic Documentation](https://wiki.openstack.org/wiki/Ironic)




### Community

#### [Twitter](https://twitter.com/metal3_io)

#### [Mailing List](https://groups.google.com/forum/#!forum/metal3-dev)

#### Join [#cluster-api-baremetal](https://kubernetes.slack.com/messages/CHD49TLE7) channel on Kunernetes Slack

#### [Community Meeting Notes](https://docs.google.com/document/d/1d7jqIgmKHvOdcEmE2v72WDZo9kz7WwhuslDOili25Ls/edit)

#### [Community Meeting](https://zoom.us/j/97255696401?pwd=ZlJMckNFLzdxMDNZN2xvTW5oa2lCZz09)

#### [Metal3 Documentation](https://metal3.io/documentation.html)


