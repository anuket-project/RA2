Conformance
===========

Traceability Matrix
-------------------

Kubernetes API testing
~~~~~~~~~~~~~~~~~~~~~~

The primary objectives of the `e2e
tests <https://github.com/kubernetes/community/blob/master/contributors/devel/sig-testing/e2e-tests.md>`__
are to ensure a consistent and reliable behavior of the Kubernetes code
base, and to catch hard-to-test bugs before users do, when unit and
integration tests are insufficient. They are partially selected for the
`Software Conformance Certification
program <https://github.com/cncf/k8s-conformance>`__ run by the
Kubernetes community (under the aegis of the CNCF).

Anuket shares the same goal to give end users the confidence that when
they use a certified product they can rely on a high level of common
functionality. Then Anuket RC2 starts with the test list defined by `K8s
Conformance <https://github.com/cncf/k8s-conformance>`__ which is
expected to grow according to the ongoing requirement traceability.

`End-to-End
Testing <https://github.com/kubernetes/community/blob/master/contributors/devel/sig-testing/e2e-tests.md>`__
basically asks for focus and skip regexes to select or to exclude
single tests:

-  focus basically matches Conformance or `Testing Special Interest
   Groups <https://github.com/kubernetes/community/blob/master/sig-testing/charter.md>`__
   in sub-sections below
-  skip excludes the SIG labels listed as optional in
   :ref:`chapters/chapter06:api and feature testing requirements`.

The Reference Conformance suites must be stable and executed on real
deployments. Then all the following labels are defacto skipped in
`End-to-End
Testing <https://github.com/kubernetes/community/blob/master/contributors/devel/sig-testing/e2e-tests.md>`__:

-  alpha
-  Disruptive
-  Flaky

It's worth mentioning that no alpha or Flaky test can be included in
Conformance as per the rules.

K8s Conformance
^^^^^^^^^^^^^^^

It must be noted that the default `K8s
Conformance <https://github.com/cncf/k8s-conformance>`__ testing is
disruptive thus Anuket RC2 rather picks
`non-disruptive-conformance <https://sonobuoy.io/docs/main/e2eplugin/>`__
testing as defined by `Sonobuoy <https://sonobuoy.io/>`__.

focus: `Conformance <#conformance>`__

skip:

-  [Disruptive]
-  NoExecuteTaintManager

API Machinery Testing
^^^^^^^^^^^^^^^^^^^^^

focus: [sig-api-machinery]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]
-  [Feature:CrossNamespacePodAffinity]
-  [Feature:CustomResourceValidationExpressions]
-  [Feature:StorageVersionAPI]
-  [Feature:WatchList]

See `API Machinery Special Interest
Group <https://github.com/kubernetes/community/tree/master/sig-api-machinery>`__
and :ref:`chapters/chapter06:api and feature testing requirements` for more details.

Apps Testing
^^^^^^^^^^^^

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

See `Apps Special Interest
Group <https://github.com/kubernetes/community/tree/master/sig-apps>`__
and :ref:`chapters/chapter06:api and feature testing requirements` for more details.

Auth Testing
^^^^^^^^^^^^

focus: [sig-auth]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]
-  [Feature:BoundServiceAccountTokenVolume]
-  [Feature:ClusterTrustBundle]
-  [Feature:PodSecurityPolicy]

See `Auth Special Interest
Group <https://github.com/kubernetes/community/tree/master/sig-auth>`__
and :ref:`chapters/chapter06:api and feature testing requirements` for more details.

Cluster Lifecycle Testing
^^^^^^^^^^^^^^^^^^^^^^^^^

focus: [sig-cluster-lifecycle]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]

See `Cluster Lifecycle Special Interest
Group <https://github.com/kubernetes/community/tree/master/sig-cluster-lifecycle>`__
and :ref:`chapters/chapter06:api and feature testing requirements` for more details.

Instrumentation Testing
^^^^^^^^^^^^^^^^^^^^^^^

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

See `Instrumentation Special Interest
Group <https://github.com/kubernetes/community/tree/master/sig-instrumentation>`__
and :ref:`chapters/chapter06:api and feature testing requirements` for more details.

Network Testing
^^^^^^^^^^^^^^^

The regexes load.balancer, LoadBalancer and
Network.should.set.TCP.CLOSE_WAIT.timeout are currently skipped because
they haven't been covered successfully neither by
`sig-release-1.29-blocking <https://github.com/kubernetes/test-infra/blob/master/config/jobs/kubernetes/sig-release/release-branch-jobs/1.29.yaml>`__
nor by `Anuket RC2
verification <http://104.154.71.112:8080/job/functest-kubernetes-v1.29-daily>`__

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

See `Network Special Interest
Group <https://github.com/kubernetes/community/tree/master/sig-network>`__
and :ref:`chapters/chapter06:api and feature testing requirements`.

Node Testing
^^^^^^^^^^^^

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

See `Node Special Interest
Group <https://github.com/kubernetes/community/tree/master/sig-node>`__
and :ref:`chapters/chapter06:api and feature testing requirements`.

Scheduling Testing
^^^^^^^^^^^^^^^^^^

focus: [sig-scheduling]

skip:

-  [alpha]
-  [Disruptive]
-  [Flaky]
-  [Feature:GPUDevicePlugin]
-  [Feature:Recreate]

See `Scheduling Special Interest
Group <https://github.com/kubernetes/community/tree/master/sig-scheduling>`__
and :ref:`chapters/chapter06:api and feature testing requirements`.

Storage Testing
^^^^^^^^^^^^^^^

It should be noted that all in-tree driver testing, [Driver:+], is
skipped. Conforming to `the upstream
gate <https://github.com/kubernetes/test-infra/blob/master/config/jobs/kubernetes/sig-release/release-branch-jobs/1.29.yaml>`__,
all PersistentVolumes NFS testing is also skipped. The following
exclusions are about `the deprecated in-tree GitRepo volume
type <https://github.com/kubernetes-sigs/kind/issues/2356>`__:

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

See `Storage Special Interest
Group <https://github.com/kubernetes/community/tree/master/sig-storage>`__
and :ref:`chapters/chapter06:api and feature testing requirements`.

Kubernetes API benchmarking
~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Rally <https://github.com/openstack/rally>`__ is a tool and framework
that performs Kubernetes API benchmarking.

`Functest Kubernetes
Benchmarking <https://git.opnfv.org/functest-kubernetes/tree/docker/benchmarking/testcases.yaml?h=stable%2Fv1.29>`__
proposed a Rally-based test case,
`xrally_kubernetes_full <https://artifacts.opnfv.org/functest-kubernetes/671YK0WH9PRK/functest-kubernetes-opnfv-functest-kubernetes-benchmarking-v1.29-xrally_kubernetes_full-run-9/xrally_kubernetes_full/xrally_kubernetes_full.html>`__,
which iterates 10 times the mainline
`xrally-kubernetes <https://github.com/xrally/xrally-kubernetes>`__
scenarios.

At the time of writing, no KPI is defined in :ref:`chapters/chapter01:introduction`
which would have asked for an update of the default SLA (maximum failure
rate of 0%) proposed in `Functest Kubernetes
Benchmarking <https://git.opnfv.org/functest-kubernetes/tree/docker/benchmarking/testcases.yaml?h=stable%2Fv1.29>`__

`Functest
xrally_kubernetes_full <https://artifacts.opnfv.org/functest-kubernetes/671YK0WH9PRK/functest-kubernetes-opnfv-functest-kubernetes-benchmarking-v1.29-xrally_kubernetes_full-run-9/xrally_kubernetes_full/xrally_kubernetes_full.html>`__:

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
~~~~~~~~~~~~~~~~~~~~~~

`Kubernetes perf-tests
repository <https://github.com/kubernetes/perf-tests>`__ hosts various
Kubernetes-related performance test related tools especially
`netperf <https://github.com/kubernetes/perf-tests/tree/master/network/benchmarks/netperf>`__
which benchmarks Kubernetes networking performance.

As listed in `netperf's
README <https://github.com/kubernetes/perf-tests/tree/master/network/benchmarks/netperf>`__,
the 5 major network traffic paths are combination of pod IP vs virtual
IP and whether the pods are co-located on the same node versus a
remotely located pod:

-  same node using pod IP
-  same node using cluster/virtual IP
-  remote node using pod IP
-  remote node using cluster/virtual IP
-  same node pod hairpin to itself using cluster/virtual IP

It should be noted that
`netperf <https://github.com/kubernetes/perf-tests/tree/master/network/benchmarks/netperf>`__
leverages `iperf <https://github.com/esnet/iperf>`__ (both TCP and UDP
modes) and `Netperf <https://github.com/HewlettPackard/netperf/>`__.

At the time of writing, no KPI is defined in Anuket chapters which would
have asked for an update of the default SLA proposed in `Functest
Kubernetes
Benchmarking <https://git.opnfv.org/functest-kubernetes/tree/docker/benchmarking?h=stable/v1.29>`__.

Security testing
~~~~~~~~~~~~~~~~

There are a couple of opensource tools that help securing the Kubernetes
stack. Amongst them, `Functest Kubernetes
Security <https://git.opnfv.org/functest-kubernetes/tree/docker/security/testcases.yaml?h=stable%2Fv1.29>`__
offers two test cases based on
`kube-hunter <https://github.com/aquasecurity/kube-hunter>`__ and
`kube-bench <https://github.com/aquasecurity/kube-bench>`__.

`kube-hunter <https://github.com/aquasecurity/kube-hunter>`__ hunts for
security weaknesses in Kubernetes clusters and
`kube-bench <https://github.com/aquasecurity/kube-bench>`__ checks
whether Kubernetes is deployed securely by running the checks documented
in the `CIS Kubernetes
Benchmark <https://www.cisecurity.org/benchmark/kubernetes/>`__.

`kube-hunter <https://github.com/aquasecurity/kube-hunter>`__ classifies
all vulnerabilities as low, medium, and high. In context of this
conformance suite, all vulnerabilities are only printed for information.

Here are the `vulnerability
categories <https://github.com/aquasecurity/kube-hunter/blob/v0.6.8/kube_hunter/core/events/types.py>`__
tagged as high by
`kube-hunter <https://github.com/aquasecurity/kube-hunter>`__:

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
it would have required an update of the default kube-bench behavior (all
failures and warnings are only printed) as integrated in `Functest
Kubernetes
Security <https://git.opnfv.org/functest-kubernetes/tree/docker/security/testcases.yaml?h=stable%2Fv1.29>`__.

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
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Running opensource containerized network functions (CNF) is a key
technical solution to ensure that the platforms meet Network Functions
Virtualization requirements.

Functest CNF offers 2 test cases which automatically onboard and test
`Clearwater IMS <https://github.com/Metaswitch/clearwater-docker>`__ via
kubectl and Helm. It’s worth mentioning that this CNF is covered by the
upstream tests (see
`clearwater-live-test <https://github.com/Metaswitch/clearwater-live-test>`__).

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
---------------------------------------

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
---------------------------

At the time of writing, the CI description file is hosted in Functest
and only runs the containers selected by Anuket RC2. It will be
completed by the next Anuket mandatory test cases and then a new CI
description file will be proposed in a shared tree.

`Xtesting CI <https://galaxy.ansible.com/collivier/xtesting>`__ only
requires internet access, GNU/Linux as Operating System and asks for a
few dependencies as described in `Deploy your own Xtesting CI/CD
toolchains <https://github.com/collivier/ansible-role-xtesting>`__:

-  python-virtualenv
-  git

Please note the next two points depending on the GNU/Linux distributions
and the network settings:

-  SELinux: you may have to add --system-site-packages when creating the
   virtualenv (“Aborting, target uses selinux but python bindings
   (libselinux-python) aren’t installed!”)
-  Proxy: you may set your proxy in env for Ansible and in systemd for
   Docker https://docs.docker.com/config/daemon/systemd/#httphttps-proxy

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
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Place the kubeconfig configuration file corresponding to the Kubernetes
cluster under test in the following location on the machine running the
cookbook:

``/home/opnfv/functest-kubernetes/config``

Run Kubernetes conformance suite
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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
