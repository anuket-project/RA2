API and Feature Testing requirements
====================================

Introduction to API and Feature Testing requirement
---------------------------------------------------

The CNCF has defined a :cite:p:`k8s-testing-sig` to help the community to write and run tests, and to contribute,
analyze, and act upon test results. This chapter maps the requirements written in the previous chapters as mandatory
Special Interest Group features. It enforces the overall requirements traceability to testing, especially those offered
for :cite:p:`k8s-testing-sig-e2e-tests`.
The Anuket Reference Conformance testing matches the features and tests defined here.

Kubernetes feature gate policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:cite:p:`k8s-feature-gates` are a set of key-value pairs that describe the Kubernetes features. The components of the
control plane of the Kubernetes Clusters can be run with different Feature Gate settings.

A feature can be in the Alpha, Beta, or General Availability (GA) stage:

- Alpha features are disabled by default. Breaking API changes may be expected. They may contain bugs, and support may
  be dropped.
- Beta features are disabled by default. They are well tested, and support will not be dropped, although breaking API
  changes may happen. As of 1.24, any existing Beta feature will continue to be enabled by default. However, new beta
  APIs and features will not be enabled by default after Kubernetes 1.24.
  For more information, see :cite:p:`k8s-kep-3136`
- GA features are stable. They are always enabled and cannot be disabled.

Only those Kubernetes features can be made mandatory in this Reference Architecture which are GA or were Beta before
Kubernetes 1.24.

A list of feature gates is available here :cite:p:`k8s-feature-gates`.

Kubernetes API policy
~~~~~~~~~~~~~~~~~~~~~

The :cite:p:`k8s-api` supports all operations and communications between components, and external user commands.
Everything in the Kubernetes platform is treated as an API object. Different API versions indicate different levels of
stability and support. An API can have Alpha, Beta or Stable versions. The version of APIs that are backed by a feature
will match the stage of the feature itself (i.e. Alpha, Beta or GA or Stable).

The policy for RA2 to include Kubernetes APIs as mandatory is as follows:

In these Reference Architecture APIs, only those APIs which are in any of the following stages are mandatory:

- Stable.
- Beta when introduced before Kubernetes version 1.24.
- Alpha or Beta when required by RA2 Ch4 specifications, or when included on the list of Mandatory API Groups below.

The Kubernetes API reference is available here :cite:p:`k8s-api-reference`.

The list of :cite:p:`k8s-v1.31-api-groups` that are mandatory is as follows:

.. list-table:: Mandatory API Groups
   :widths: 30 30
   :header-rows: 1

   * - Group
     - Version
   * - admissionregistration.k8s.io
     - v1
   * - apiextensions.k8s.io
     - v1
   * - apiregistration.k8s.io
     - v1
   * - apps
     - v1
   * - authentication.k8s.io
     - v1
   * - authorization.k8s.io
     - v1
   * - autoscaling
     - v1, v2
   * - batch
     - v1
   * - certificates.k8s.io
     - v1
   * - coordination.k8s.io
     - v1
   * - core
     - v1
   * - discovery.k8s.io
     - v1
   * - events.k8s.io
     - v1
   * - flowcontrol.apiserver.k8s.io
     - v1
   * - networking.k8s.io
     - v1
   * - node.k8s.io
     - v1
   * - policy
     - v1
   * - rbac.authorization.k8s.io
     - v1
   * - scheduling.k8s.io
     - v1
   * - storage.k8s.io
     - v1

API Machinery Special Interest Group :cite:p:`k8s-api-sig-api-machinery`
------------------------------------------------------------------------

.. list-table:: API Machinery Special Interest Group
   :widths: 30 10 60
   :header-rows: 1

   * - Labels
     - Mandatory
     - Description
   * - Conformance
     - X
     - Kubernetes conformance test
   * - None
     - X
     - Kubernetes mainstream features
   * - Feature:ComprehensiveNamespaceDraining
     - X
     - The deletion of namespaces should always be fast (all 100 namespaces in 150 seconds).
   * - Feature: CrossNamespacePodAffinity :cite:p:`k8s-feature-crossnamespacepodaffinity`
     -
     - The CrossNamespacePodAffinity feature verifies the ResourceQuota with the cross namespace pod affinity scope
       using scope-selectors.
   * - Feature: PodPriority :cite:p:`k8s-feature-crossnamespacepodaffinity`
     - X
     - The PodPriority feature verifies the ResourceQuota's priority class scope against a pod with a different
       priority class.
   * - Feature:ScopeSelectors
     - X
     - Verify ResourceQuota with terminating scopes through scope selectors
   * - Feature: StorageVersionAPI :cite:p:`k8s-feature-storageversionapi`
     -
     - Enable the storage version API.
   * - Feature:WatchList :cite:p:`k8s-feature-gates`
     -
     - Enable support for streaming initial state of objects in watch requests.

Apps  :cite:p:`k8s-api-sig-apps`
------------------------------------------------------

.. list-table:: Apps Special Interest Group
   :widths: 30 10 60
   :header-rows: 1

   * - Labels
     - Mandatory
     - Description
   * - Conformance
     - X
     - Kubernetes conformance test
   * - None
     - X
     - Kubernetes mainstream features
   * - Feature: DaemonSetUpdateSurge :cite:p:`k8s-feature-daemonsetupdatesurge`
     -
     - The Daemon set should surge the pods onto the nodes when the specification is updated and the update strategy is
       RollingUpdate.
   * - Feature: IndexedJob :cite:p:`k8s-feature-indexedjob`
     -
     - The IndexedJob feature should create pods for an indexed job with completion indexes.
   * - Feature: StatefulSet :cite:p:`k8s-feature-statefulset`
     -
     - The StatefulSet feature should create a working zookeeper cluster.
   * - Feature:StatefulUpgrade
     -
     - The StatefulUpgrade feature should maintain a functioning cluster.
   * - Feature: SuspendJob :cite:p:`k8s-feature-suspendjob`
     -
     - The SuspendJob feature should not create pods when they have been created in a suspended state.
   * - Feature: TaintEviction :cite:p:`k8s-feature-tainteviction`
     -
     - All pods on the unreachable node should be marked as NotReady when the node condition is set to NotReady. All
       pods should be evicted after eviction timeout has passed.
   * - Feature: TTLAfterFinished :cite:p:`k8s-feature-ttlafterfinished`
     - X
     - The job should be deleted once it has finished, after the TTL has elapsed.

Auth Special Interest Group :cite:p:`k8s-api-sig-auth`
------------------------------------------------------

.. list-table:: Auth Special Interest Group
   :widths: 30 10 60
   :header-rows: 1

   * - Labels
     - Mandatory
     - Description
   * - Conformance
     - X
     - Kubernetes conformance test
   * - None
     - X
     - Kubernetes mainstream features
   * - Feature: BoundServiceAccountTokenVolume :cite:p:`k8s-feature-boundserviceaccounttokenvolume`
     -
     - The ServiceAccount admission controller migration upgrade should maintain a functioning cluster.
   * - Feature:ClusterTrustBundle :cite:p:`k8s-feature-gates`
     -
     - Enable ClusterTrustBundle objects and kubelet integration.
   * - Feature:NodeAuthenticator
     - X
     - The kubelet's main port 10250 should reject requests with no credentials.
   * - Feature:NodeAuthorizer
     - X
     - Setting existing and non-existent attributes should return with a Forbidden error, not a NotFound error.
   * - NodeFeature:FSGroup
     - X
     - ServiceAccounts should set ownership and permission when RunAsUser or FsGroup is present.

Cluster Lifecycle Special Interest Group :cite:p:`k8s-api-sig-cluster-lifecycle`
--------------------------------------------------------------------------------

.. list-table:: Cluster Lifecycle Special Interest Group
   :widths: 30 10 60
   :header-rows: 1

   * - Labels
     - Mandatory
     - Description
   * - Conformance
     - X
     - Kubernetes conformance test
   * - None
     - X
     - Kubernetes mainstream features
   * - Feature:BootstrapTokens
     - X
     - The BootstrapTokens feature should delete the token secret when the secret has expired.


Instrumentation Special Interest Group :cite:p:`k8s-api-sig-instrumentation`
----------------------------------------------------------------------------

.. list-table:: Instrumentation Special Interest Group
   :widths: 30 10 60
   :header-rows: 1

   * - Labels
     - Mandatory
     - Description
   * - Conformance
     - X
     - Kubernetes conformance test
   * - None
     - X
     - Kubernetes mainstream features
   * - Feature:Elasticsearch
     -
     - The Elasticsearch feature should check that the Kibana logging instance is alive.
   * - Feature: StackdriverAcceleratorMonitoring
     -
     - Stackdriver Monitoring should have accelerator metrics.
   * - Feature:StackdriverCustomMetrics
     -
     - Stackdriver Monitoring should run Custom Metrics - Stackdriver Adapter for the new resource model.
   * - Feature:StackdriverExternalMetrics
     -
     - Stackdriver Monitoring should run Custom Metrics - Stackdriver Adapter for external metrics.
   * - Feature:StackdriverMetadataAgent
     -
     - Stackdriver Monitoring should run Stackdriver Metadata Agent.
   * - Feature:StackdriverMonitoring
     -
     -

Network Special Interest Group :cite:p:`k8s-api-sig-network`
------------------------------------------------------------

.. list-table:: Network Special Interest Group
   :widths: 30 10 60
   :header-rows: 1

   * - Labels
     - Mandatory
     - Description
   * - Conformance
     - X
     - Kubernetes conformance test.
   * - None
     - X
     - Kubernetes mainstream features.
   * - Feature:Example
     -
     - The example feature should create a pod that uses DNS.
   * - Feature:Ingress
     -
     - The Ingress feature should prevent ingress creation if more than one IngressClass is marked as a default.
   * - Feature: IPv6DualStack :cite:p:`k8s-feature-ipv6dualstack`
     -
     - IPv4/IPv6 dual-stack networking enables the allocation of both IPv4 and IPv6 addresses to Pods and Services.
       IPv4/IPv6 dual-stack networking is enabled by default for your Kubernetes cluster from 1.21 onwards, allowing
       the simultaneous assignment of IPv4 and IPv6 addresses.
   * - Feature:kubemci
     -
     - The kubemci feature should create ingress with a preshared certificate.
   * - Feature:KubeProxyDaemonSetMigration
     -
     - The upgrade of kube-proxy from static pods to a DaemonSet should maintain a functioning cluster.
   * - Feature:KubeProxyDaemonSetUpgrade
     -
     - The upgrade of kube-proxy from static pods to a DaemonSet should maintain a functioning cluster.
   * - Feature:NEG
     -
     - The NEG feature should sync the endpoints to NEG.
   * - Feature:NoSNAT
     - X
     - The NoSNAT feature should be able to send traffic between the Pods without SNAT.
   * - Feature:Networking-IPv4
     - X
     - Networking-IPv4 should provide an IPv4 connection for the containers.
   * - Feature:Networking-IPv6
     -
     - Networking-IPv6 should provide an IPv6 connection for the containers.
   * - Feature:Networking-Performance
     - X
     - Measure network responsiveness, latency (both RTT and OWD), and throughput with the iperf2 tool.
   * - Feature:NetworkPolicy
     -
     - NetworkPolicy between the server and the client should enforce a policy to allow traffic only from a different
       namespace, based on NamespaceSelector.
   * - Feature:PerformanceDNS
     -
     - The PerformanceNDS feature should answer DNS queries for a maximum number of services per cluster.
   * - Feature:SCTP
     -
     - SCTP should allow the creation of a basic SCTP service with the pod and the endpoints.
   * - Feature:SCTPConnectivity
     -
     - The Pods should function for intra-pod communication: sctp.
   * - Feature:ServiceCIDRs :cite:p:`k8s-extend-service-ip-ranges`
     -
     - Track IP address allocations for Service cluster IPs using IPAddress objects.

Node Special Interest Group :cite:p:`k8s-api-sig-node`
------------------------------------------------------

.. list-table:: Node Special Interest Group
   :widths: 30 10 60
   :header-rows: 1

   * - Labels
     - Mandatory
     - Description
   * - Conformance
     - X
     - Kubernetes conformance test.
   * - None
     - X
     - Kubernetes mainstream features.
   * - Feature:DynamicResourceAllocation :cite:p:`k8s-feature-gates`
     -
     - Enables support for resources with custom parameters and a lifecycle that is independent of a Pod.
   * - Feature:Example
     - X
     - The liveness pods should be automatically restarted.
   * - Feature: ExperimentalResourceUsageTracking
     -
     - Resource tracking for 100 pods per node.
   * - Feature:GPUUpgrade
     -
     - The Control Plane node upgrade should not disrupt the GPU Pod.
   * - Feature:InPlacePodVerticalScaling :cite:p:`k8s-feature-gates`
     -
     - Enables in-place Pod vertical scaling.
   * - Feature:NodeLogQuery :cite:p:`k8s-feature-gates`
     -
     - Enables querying logs of node services using the /logs endpoint.
   * - Feature:PodGarbageCollector
     -
     - The PodGarbageCollector feature should handle the creation of 1000 pods.
   * - Feature:PodLifecycleSleepAction :cite:p:`k8s-feature-gates`
     -
     - Enables the sleep action in Container lifecycle hooks.
   * - Feature:RegularResourceUsageTracking
     -
     - Resource tracking for 0 pods per node.
   * - Feature:SidecarContainers :cite:p:`k8s-feature-gates`
     -
     - Allow setting the restartPolicy of an init container to Always so that
       the container becomes a sidecar container (restartable init containers).
   * - Feature:UserNamespacesSupport :cite:p:`k8s-feature-gates`
     -
     - Enable user namespace support for Pods.
   * - Feature: ProbeTerminationGracePeriod :cite:p:`k8s-feature-probeterminationgraceperiod`
     - X
     - The probing container should override timeoutGracePeriodSeconds when the LivenessProbe field is set.
   * - NodeFeature: DownwardAPIHugePages :cite:p:`k8s-feature-downwardapihugepages`
     -
     - Downward API tests for huge pages should provide the container's limits.hugepages-pagesize, and
       requests.hugepages-pagesize as environmental variables.
   * - NodeFeature: PodReadinessGate :cite:p:`k8s-feature-podreadinessgate`
     - X
     - The Pods should support the pod readiness gates.
   * - NodeFeature:RuntimeHandler
     -
     - The RuntimeClass feature should run a Pod requesting a RuntimeClass with a configured handler.
   * - NodeFeature: Sysctls :cite:p:`k8s-feature-sysctls`
     - X
     - The Sysctls feature should not launch unsafe, but not explicitly enabled sysctls on the node.

Scheduling Special Interest Group :cite:p:`k8s-api-sig-scheduling`
------------------------------------------------------------------

.. list-table:: Scheduling Special Interest Group
   :widths: 30 10 60
   :header-rows: 1

   * - Labels
     - Mandatory
     - Description
   * - Conformance
     - X
     - Kubernetes conformance test.
   * - None
     - X
     - Kubernetes mainstream features.
   * - Feature:GPUDevicePlugin
     -
     - The GPUDevicePlugin feature runs Nvidia GPU Device Plugin tests.
   * - Feature: LocalStorageCapacityIsolation :cite:p:`k8s-feature-localstoragecapacityisolation`
     - X
     - The LocalStorageCapacityIsolation feature validates local ephemeral storage resource limits of pods
       that are allowed to run.
   * - Feature:Recreate
     -
     - The Recreate feature runs Nvidia GPU Device Plugin tests with a recreation.

Storage Special Interest Group :cite:p:`k8s-api-sig-storage`
------------------------------------------------------------

.. list-table:: Storage Special Interest Group
   :widths: 30 10 60
   :header-rows: 1

   * - Labels
     - Mandatory
     - Description
   * - Conformance
     - X
     - Kubernetes conformance test.
   * - None
     - X
     - Kubernetes mainstream features.
   * - Feature:ExpandInUsePersistentVolumes
     -
     -
   * - Feature:Flexvolumes
     -
     -
   * - Feature:RecoverVolumeExpansionFailure :cite:p:`k8s-feature-gates`
     -
     - Enables users to edit their PVCs to smaller sizes so as they can
       recover from previously issued volume expansion failures.
   * - Feature:SELinux
     -
     -
   * - Feature:GKELocalSSD
     -
     -
   * - Feature:VolumeSnapshotDataSource
     -
     -
   * - Feature:Volumes
     - X
     -
   * - Feature:vsphere
     -
     -
   * - Feature:Windows
     -
     -
   * - NodeFeature:EphemeralStorage
     - X
     -
   * - NodeFeature:FSGroup
     - X
     -

Conformance testing
-------------------

The objective of this section is to provide an automated mechanism
to validate Kubernetes based cloud infrastructure
against the standard set of requirements defined in
:ref:`chapters/chapter02:architecture requirements`. Through this validation
mechanism, a provider of cloud infrastructure will be able to test their
cloud infrastructure's conformance to this reference architecture. This will
ease the integration of network functions into operator environments that host
compatible cloud infrastructures, thereby reducing cost, complexity, and time
of integration.

The overall workstream requires the close coordination of the following:

-  **Requirements** - The agreed upon capabilities and conditions that a
   compliant cloud infrastructure must provide or satisfy.
-  **Tests** - The verification mechanism that determines that a given
   cloud infrastructure complies with one or more requirements.
-  **Conformance Specifications** - The definition of the requirements,
   tests, and circumstances (test case integration, etc.) that must be
   met to be deemed conformant.

Requirements and Testing Principles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In addition to the description of the test case integration and tooling,
Cloud Infrastructure Reference Architecture managed by OpenStack
:cite:p:`refarch1` defines the requirements and the testing principles to
which every Anuket Conformance test suite must comply as this one for
Kubernetes.

In two words, the verification, validation, and conformance processes leverage
existing Anuket testing knowledge (projects) and experience (history) by
utilising the toolchain design already in-place.

The Kubernetes based cloud infrastructure suite
**MUST** utilise the Anuket test case integration toolchain to deliver
overall integration, the same end user actions, and a unique test result
format (e.g. Anuket test result database) needed by the end users and any
test case result verification program.

To reach all goals in terms of verification, validation, compliance, and
conformance, all test cases **MUST** be delivered as Docker containers
:cite:p:`docker` to simplify the CI toolchain
setup including:

-  the common test case execution
-  the unified way to manage all the interactions with the CI/CD
   components and with third-parties (e.g. dump all test case logs and
   results for conformance)

The Docker containers proposed by the test projects **MUST** also embed the
Xtesting Python package :cite:p:`xtestingpythonpackage` and the
related test case execution description files
:cite:p:`testcasedescription` as required by Xtesting.

Xtesting CI :cite:p:`xtestingci`
leverages the common test case execution proposed by Xtesting. Thanks to
a simple test case list, this tool deploys plug-and-play CI/CD
toolchains in a few commands :cite:p:`cicdtoolchainsinafewcommands` to
run this Conformance testing.

See Cloud Infrastructure Reference Architecture managed by OpenStack
:cite:p:`refarch1` for more details.

Test Case traceability
~~~~~~~~~~~~~~~~~~~~~~

Kubernetes API testing
^^^^^^^^^^^^^^^^^^^^^^

The primary objectives of the e2e tests :cite:p:`k8s-testing-sig-e2e-tests`
are to ensure a consistent and reliable behavior of the Kubernetes code
base, and to catch hard-to-test bugs before users do, when unit and
integration tests are insufficient. They are partially selected for the
Software Conformance Certification program
:cite:p:`k8s-conformance` run by the Kubernetes community (under the aegis of
the CNCF).

Anuket shares the same goal to give end users the confidence that when
they use a certified product they can rely on a high level of common
functionality. Then the Conformance testing starts with the test list defined
by the Certified Kubernetes Conformance Program :cite:p:`k8s-conformance`
which is expected to grow according to the ongoing requirement traceability.

End-to-End Testing :cite:p:`k8s-testing-sig-e2e-tests` basically asks for
focus and skip regexes to select or to exclude single tests:

-  focus basically matches Conformance or Testing Special Interest
   Groups :cite:p:`k8s-testing-sig` in sub-sections below
-  skip excludes the SIG labels listed as optional in
   :ref:`chapters/chapter06:api and feature testing requirements`.

The Reference Conformance suites must be stable and executed on real
deployments. Then all the following labels are defacto skipped in
the End-to-End Testing :cite:p:`k8s-testing-sig-e2e-tests`:

-  alpha
-  Disruptive
-  Flaky

It's worth mentioning that no alpha or Flaky test can be included in
Conformance as per the rules.

K8s Conformance
+++++++++++++++

It must be noted that the default K8s Conformance :cite:p:`k8s-conformance`
testing is disruptive thus this Conformance testing rather picks
non-disruptive-conformance :cite:p:`non-disruptive-conformance` testing as
defined by Sonobuoy :cite:p:`sonobuoy`.

focus: [Conformance]

skip:

-  [Disruptive]
-  NoExecuteTaintManager

API Machinery Testing
+++++++++++++++++++++

focus: [sig-api-machinery]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]
-  [Feature:CrossNamespacePodAffinity]
-  [Feature:CustomResourceValidationExpressions]
-  [Feature:StorageVersionAPI]
-  [Feature:WatchList]

See API Machinery Special Interest Group :cite:p:`k8s-api-sig-api-machinery`
and :ref:`chapters/chapter06:api and feature testing requirements` for more
details.

Apps Testing
++++++++++++

focus: [sig-apps]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]
-  [Feature:DaemonSetUpdateSurge]
-  [Feature:IndexedJob]
-  [Feature:StatefulSet]
-  [Feature:StatefulSetAutoDeletePVC]
-  [Feature:StatefulUpgrade]
-  [Feature:SuspendJob]

See Apps Special Interest Group :cite:p:`k8s-api-sig-apps`
and :ref:`chapters/chapter06:api and feature testing requirements`
for more details.

Auth Testing
++++++++++++

focus: [sig-auth]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]
-  [Feature:BoundServiceAccountTokenVolume]
-  [Feature:ClusterTrustBundle]
-  [Feature:PodSecurityPolicy]

See Auth Special Interest Group :cite:p:`k8s-api-sig-auth`
and :ref:`chapters/chapter06:api and feature testing requirements`
for more details.

Cluster Lifecycle Testing
+++++++++++++++++++++++++

focus: [sig-cluster-lifecycle]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]

See Cluster Lifecycle Special Interest Group
:cite:p:`k8s-api-sig-cluster-lifecycle`
and :ref:`chapters/chapter06:api and feature testing requirements`
for more details.

Instrumentation Testing
+++++++++++++++++++++++

focus: [sig-instrumentation]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]
-  [Feature:Elasticsearch]
-  [Feature:StackdriverAcceleratorMonitoring]
-  [Feature:StackdriverCustomMetrics]
-  [Feature:StackdriverExternalMetrics]
-  [Feature:StackdriverMetadataAgent]
-  [Feature:StackdriverMonitoring]

See Instrumentation Special Interest Group
:cite:p:`k8s-api-sig-instrumentation`
and :ref:`chapters/chapter06:api and feature testing requirements`
for more details.

Network Testing
+++++++++++++++

The regexes load.balancer, LoadBalancer and
Network.should.set.TCP.CLOSE_WAIT.timeout are currently skipped because
they haven't been covered successfully neither by
the upstream kubernetes gate :cite:p:`upstream-kubernetes-gate` nor by the
Anuket verification :cite:p:`anuket-rc2-verification`.

Please note that a couple of tests must be skipped by name below as they
are no appropriate labels.

focus: [sig-network]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]
-  [Feature:Example]
-  [Feature:Ingress]
-  [Feature:IPv6DualStack]
-  [Feature:kubemci]
-  [Feature:KubeProxyDaemonSetMigration]
-  [Feature:KubeProxyDaemonSetUpgrade]
-  [Feature:NEG]
-  [Feature:Networking-IPv6]
-  [Feature:NetworkPolicy]
-  [Feature:PerformanceDNS]
-  [Feature:ProxyTerminatingEndpoints]
-  [Feature:SCTP]
-  [Feature:SCTPConnectivity]
-  [Feature:ServiceCIDRs]
-  DNS configMap nameserver
-  load.balancer
-  LoadBalancer
-  Network.should.set.TCP.CLOSE_WAIT.timeout

See Network Special Interest Group :cite:p:`k8s-api-sig-network`
and :ref:`chapters/chapter06:api and feature testing requirements`
for more details.

Node Testing
++++++++++++

focus: [sig-node]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]
-  [Feature:DynamicResourceAllocation]
-  [Feature:ExperimentalResourceUsageTracking]
-  [Feature:GRPCContainerProbe]
-  [Feature:GPUUpgrade]
-  [Feature:InPlacePodVerticalScaling]
-  [Feature:KubeletCredentialProviders]
-  [Feature:NodeLogQuery]
-  [Feature:PodGarbageCollector]
-  [Feature:PodLifecycleSleepAction]
-  [Feature:RegularResourceUsageTracking]
-  [Feature:SidecarContainers]
-  [Feature:UserNamespacesSupport]
-  [Feature:UserNamespacesStatelessPodsSupport]
-  [NodeFeature:DownwardAPIHugePages]
-  [NodeFeature:RuntimeHandler]

See Node Special Interest Group :cite:p:`k8s-api-sig-node`
and :ref:`chapters/chapter06:api and feature testing requirements`
for more details.

Scheduling Testing
++++++++++++++++++

focus: [sig-scheduling]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]
-  [Feature:GPUDevicePlugin]
-  [Feature:Recreate]

See Scheduling Special Interest Group
:cite:p:`k8s-api-sig-scheduling`
and :ref:`chapters/chapter06:api and feature testing requirements`
for more details.

Storage Testing
+++++++++++++++

It should be noted that all in-tree driver testing, [Driver:+], is
skipped. Conforming to the upstream gate :cite:p:`upstream-kubernetes-gate`,
all PersistentVolumes NFS testing is also skipped. The following
exclusions are about the deprecated in-tree GitRepo volume
type :cite:p:`deprecated-in-tree-gitrepo-volume-type`:

-  should provision storage with different parameters
-  should not cause race condition when used for git_repo

Please note that a couple of tests must be skipped by name below as they
are no appropriate labels.

focus: [sig-storage]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]
-  [Driver:+]
-  [Feature:ExpandInUsePersistentVolumes]
-  [Feature:Flexvolumes]
-  [Feature:GKELocalSSD]
-  [Feature:VolumeSnapshotDataSource]
-  [Feature:Flexvolumes]
-  [Feature:RecoverVolumeExpansionFailure]
-  [Feature:SELinux]
-  [Feature:vsphere]
-  [Feature:Volumes]
-  [Feature:Windows]
-  [NodeFeature:EphemeralStorage]
-  PersistentVolumes.NFS
-  should provision storage with different parameters
-  should not cause race condition when used for git_repo

See Storage Special Interest Group :cite:p:`k8s-api-sig-storage`
and :ref:`chapters/chapter06:api and feature testing requirements`
for more details.

Kubernetes API benchmarking
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Rally :cite:p:`xrally-kubernetes` is a tool and framework
that performs Kubernetes API benchmarking.

Functest Kubernetes Benchmarking :cite:p:`functest-kubernetes-benchmarking`
proposed a Rally-based test case, xrally_kubernetes_full
:cite:p:`xrally-kubernetes-full`, which iterates 10 times the mainline
xrally-kubernetes :cite:p:`xrally-kubernetes` scenarios.

At the time of writing, no KPI is defined in
:ref:`chapters/chapter02:architecture requirements`
which would have asked for an update of the default SLA (maximum failure
rate of 0%) proposed in Functest Kubernetes Benchmarking
:cite:p:`functest-kubernetes-benchmarking`

Functest xrally_kubernetes_full :cite:p:`functest-kubernetes-benchmarking`:

.. list-table:: Kubernetes API benchmarking
   :widths: 80 20
   :header-rows: 1

   * - Scenarios
     - Iterations
   * - Kubernetes.create_and_delete_deployment
     - 10
   * - Kubernetes.create_and_delete_job
     - 10
   * - Kubernetes.create_and_delete_namespace
     - 10
   * - Kubernetes.create_and_delete_pod
     - 10
   * - Kubernetes.create_and_delete_pod_with_configmap_volume
     - 10
   * - Kubernetes.create_and_delete_pod_with_configmap_volume [2]
     - 10
   * - Kubernetes.create_and_delete_pod_with_emptydir_volume
     - 10
   * - Kubernetes.create_and_delete_pod_with_emptydir_volume [2]
     - 10
   * - Kubernetes.create_and_delete_pod_with_hostpath_volume
     - 10
   * - Kubernetes.create_and_delete_pod_with_secret_volume
     - 10
   * - Kubernetes.create_and_delete_pod_with_secret_volume [2]
     - 10
   * - Kubernetes.create_and_delete_replicaset
     - 10
   * - Kubernetes.create_and_delete_replication_controller
     - 10
   * - Kubernetes.create_and_delete_statefulset
     - 10
   * - Kubernetes.create_check_and_delete_pod_with_cluster_ip_service
     - 10
   * - Kubernetes.create_check_and_delete_pod_with_cluster_ip_service [2]
     - 10
   * - Kubernetes.create_check_and_delete_pod_with_node_port_service
     - 10
   * - Kubernetes.create_rollout_and_delete_deployment
     - 10
   * - Kubernetes.create_scale_and_delete_replicaset
     - 10
   * - Kubernetes.create_scale_and_delete_replication_controller
     - 10
   * - Kubernetes.create_scale_and_delete_statefulset
     - 10
   * - Kubernetes.list_namespaces
     - 10

The following software versions are considered to benchmark Kubernetes
v1.29 (latest stable release) selected by Anuket:

.. list-table:: Software versions
   :widths: 50 50
   :header-rows: 1

   * - Software
     - Version
   * - Functest
     - v1.29
   * - xrally-kubernetes
     - 1.1.1.dev14+g2ffa85a

Dataplane benchmarking
^^^^^^^^^^^^^^^^^^^^^^

Kubernetes perf-tests repository :cite:p:`kubernetes-perf-tests-repository`
hosts various Kubernetes-related performance test related tools especially
netperf :cite:p:`kubernetes-netperf` which benchmarks Kubernetes networking
performance.

As listed in netperf's README :cite:p:`kubernetes-netperf`'s README,
the 5 major network traffic paths are combination of pod IP vs virtual
IP and whether the pods are co-located on the same node versus a
remotely located pod:

-  same node using pod IP
-  same node using cluster/virtual IP
-  remote node using pod IP
-  remote node using cluster/virtual IP
-  same node pod hairpin to itself using cluster/virtual IP

It should be noted that netperf :cite:p:`kubernetes-netperf` leverages
iperf :cite:p:`iperf` (both TCP and UDP modes) and Netperf :cite:p:`netperf`.

At the time of writing, no KPI is defined in Anuket chapters which would
have asked for an update of the default SLA proposed in
Functest Kubernetes Benchmarking :cite:p:`functest-kubernetes-benchmarking`.

Security testing
^^^^^^^^^^^^^^^^

There are a couple of opensource tools that help securing the Kubernetes
stack. Amongst them, Functest Kubernetes Security
:cite:p:`functest-kubernetes-security`
offers two test cases based on kube-hunter :cite:p:`kube-hunter` and
kube-bench :cite:p:`kube-bench`.

kube-hunter :cite:p:`kube-hunter` hunts for security weaknesses in
Kubernetes clusters and kube-bench :cite:p:`kube-bench` checks whether
Kubernetes is deployed securely by running
the checks documented in the CIS Kubernetes Benchmark
:cite:p:`cis-kubernetes-benchmark`.

kube-hunter :cite:p:`kube-hunter` classifies all vulnerabilities as low,
medium, and high. In context of this conformance suite, all vulnerabilities
are only printed for information.

Here are the vulnerability categories :cite:p:`vulnerability-categories`
tagged as high by kube-hunter :cite:p:`kube-hunter`:

- ExposedSensitiveInterfacesTechnique
- MountServicePrincipalTechnique
- ListK8sSecretsTechnique
- InstanceMetadataApiTechnique
- ExecIntoContainerTechnique
- SidecarInjectionTechnique
- NewContainerTechnique
- GeneralPersistenceTechnique
- HostPathMountPrivilegeEscalationTechnique
- PrivilegedContainerTechnique
- ClusterAdminBindingTechnique
- CoreDNSPoisoningTechnique
- DataDestructionTechnique
- GeneralDefenseEvasionTechnique
- CVERemoteCodeExecutionCategory
- CVEPrivilegeEscalationCategory

At the time of writing, none of the Center for Internet Security (CIS)
rules are defined as mandatory (e.g., sec.std.001: The Cloud Operator
**should** comply with Center for Internet Security CIS Controls) else
it would have required an update of the default kube-bench :cite:p:`kube-bench`
behavior (all failures and warnings are only printed) as integrated in
Functest Kubernetes Security :cite:p:`functest-kubernetes-security`.

The following software versions are considered to verify Kubernetes
v1.29 (latest stable release) selected by Anuket:

.. list-table:: Software versions
   :widths: 50 50
   :header-rows: 1

   * - Software
     - Version
   * - Functest
     - v1.29
   * - kube-hunter
     - 0.6.8
   * - kube-bench
     - v0.6.10

Opensource CNF onboarding and testing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Running opensource containerized network functions (CNF) is a key
technical solution to ensure that the platforms meet Network Functions
Virtualization requirements.

Functest CNF offers 2 test cases which automatically onboard and test
Clearwater IMS :cite:p:`clearwater-ims` via kubectl and Helm. It’s worth
mentioning that this CNF is covered by the upstream tests
(see clearwater-live-test :cite:p:`clearwater-live-test`).

The following software versions are considered to verify Kubernetes
v1.29 (latest stable release) selected by Anuket:

.. list-table:: Software versions
   :widths: 50 50
   :header-rows: 1

   * - Software
     - Version
   * - Functest
     - v1.29
   * - clearwater
     - release-130
   * - Helm
     - v3.3.1

Test Cases Traceability to Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following test case must pass as they are for Reference Conformance:

.. list-table:: Mandory test cases
   :widths: 40 25 10 25
   :header-rows: 1

   * - Container
     - Test suite
     - Criteria
     - Requirements
   * - opnfv/functest-kubernetes-smoke:v1.29
     - xrally_kubernetes
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - k8s_conformance
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - k8s_conformance_serial
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_api_machinery
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_api_machinery_serial
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_apps
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_apps_serial
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_auth
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_cluster_lifecycle
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_instrumentation
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_network
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_node
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_scheduling_serial
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_storage
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-smoke:v1.29
     - sig_storage_serial
     - PASS
     - Kubernetes API testing
   * - opnfv/functest-kubernetes-security:v1.29
     - kube_hunter
     - PASS
     - Security testing
   * - opnfv/functest-kubernetes-security:v1.29
     - kube_bench_master
     - PASS
     - Security testing
   * - opnfv/functest-kubernetes-security:v1.29
     - kube_bench_node
     - PASS
     - Security testing
   * - opnfv/functest-kubernetes-benchmarking:v1.29
     - xrally_kubernetes_full
     - PASS
     - Kubernetes API benchmarking
   * - opnfv/functest-kubernetes-benchmarking:v1.29
     - netperf
     - PASS
     - Dataplane benchmarking
   * - opnfv/functest-kubernetes-cnf:v1.29
     - k8s_vims
     - PASS
     - Opensource CNF onboarding and testing
   * - opnfv/functest-kubernetes-cnf:v1.29
     - helm_vims
     - PASS
     - Opensource CNF onboarding and testing

Kubernetes Testing Cookbook
~~~~~~~~~~~~~~~~~~~~~~~~~~~

At the time of writing, the CI description file is hosted in Functest
and only runs the containers selected here. It will be
completed by the next Anuket mandatory test cases and then a new CI
description file will be proposed in a shared tree.

`Xtesting CI :cite:p:`xtestingci` only requires internet access,
GNU/Linux as Operating System and asks for a few dependencies as described in
Deploy your own Xtesting CI/CD toolchains
:cite:p:`deploy-your-own-xtesting-cicd-toolchains`:

-  python-virtualenv
-  git

Please note the next two points depending on the GNU/Linux distributions
and the network settings:

-  SELinux: you may have to add --system-site-packages when creating the
   virtualenv (“Aborting, target uses selinux but python bindings
   (libselinux-python) aren’t installed!”)
-  Proxy: you may set your proxy in env for Ansible and in  systemd for
   Docker :cite:p:`systemd-for-docker`

To deploy your own CI toolchain running Anuket Compliance:

.. code:: bash

   virtualenv functest-kubernetes --system-site-packages
   . functest-kubernetes/bin/activate
   pip install ansible
   ansible-galaxy install collivier.xtesting
   ansible-galaxy collection install ansible.posix community.general community.grafana kubernetes.core community.docker community.postgresql
   git clone https://gerrit.opnfv.org/gerrit/functest-kubernetes functest-kubernetes-src
   (cd functest-kubernetes-src && git checkout -b stable/v1.29 origin/stable/v1.29)
   ansible-playbook functest-kubernetes-src/ansible/site.cntt.yml

Configure Kubernetes API testing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Place the kubeconfig configuration file corresponding to the Kubernetes
cluster under test in the following location on the machine running the
cookbook:

``/home/opnfv/functest-kubernetes/config``

Run Kubernetes conformance suite
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Open http://127.0.0.1:8080/job/functest-kubernetes-v1.29-daily/ in a web
browser, login as admin/admin and click on “Build with Parameters” (keep
the default values).

If the System under test (SUT) is Anuket compliant, a link to the full
archive containing all test results and artifacts will be printed in
functest-kubernetes-v1.29-zip’s console. Be free to download it and then
to send it to any reviewer committee.

To clean your working dir:

.. code:: bash

   deactivate
   rm -rf functest-kubernetes-src functest-kubernetes
