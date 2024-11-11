Gaps, Innovation, and Development
=================================

Introduction to Gaps, Innovation, and Development
-------------------------------------------------

Functional gaps exist between available open-source
technology and this Reference Architecture's (RA) or
Reference Model's (RM) requirements. This chapter
details these gaps and proposes solutions.  This may
identify and target various "upstream" community
projects for development efforts.

Gap Template
~~~~~~~~~~~~

**Related requirements:** List requirement references
(e.g., ``abc.xyz.00``) from RA2 or RM addressed by this
gap.

**Baseline project:**  Identify the upstream project
(e.g., *Kubernetes*) where the gap exists. If none, state
"none".

**Gap description:** Describe missing functionality from
the related requirements in known implementations. Include
references to ongoing work in the target project that may
address the gap.


Container Run-Time Interfaces Towards NFVI Resources
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This describes the southbound interface from the container
to IaaS-provided infrastructure resources; e.g., the
network interface type presented to a running container.


Multitenancy and Workload Isolation with Kubernetes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Related requirements:** ``e.man.004``, ``sec.ci.008``,
``sec.wl.005``, ``sec.wl.006``

**Baseline project:** *Kubernetes*

**Gap description:** Kubernetes currently lacks robust
multitenancy, preventing secure infrastructure resource
sharing among untrusted tenants. This poses security risks
when separating workloads by category (e.g., production
vs. non-production).  Tenant network segmentation is also
needed, while maintaining central administration.  Beyond
security, this creates operational challenges. Deploying
many CNFs in one cluster risks version and configuration
conflicts, and software lifecycle management problems.
Lack of isolation increases cascading failure risk.

**Proposals & Resolution:** Kubernetes isn't a
single-cluster solution.  Industry case studies
(:cite:t:`alibaba-blog-twitter`, :cite:t:`youtube-zalando`,
:cite:t:`cncf-blog-alibaba`) and CNCF surveys show
growing multi-cluster deployments within organizations. A
multi-cluster approach addresses security and software
lifecycle management challenges.

Without in-cluster multitenancy, separate clusters provide
necessary CNF isolation (based on vendor, environment,
category, or independent lifecycles).  Co-locating similar
CNFs allows for simultaneous upgrades, while separate
clusters accommodate independent upgrades for CNFs with
different versions, configurations, and dependencies.

However, managing numerous clusters at scale poses
significant operational challenges if done manually.
Operators should carefully consider their multi-cluster
management strategy, including application management.


Kubernetes as a VM-based VNF Orchestrator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Related requirements:** None.

**Baseline project:** *Kubernetes*, *Kubevirt*

**Gap description:** Kubernetes and a CRI-compliant
runtime should support VNF execution without altering VNF
architecture or deployment artifacts.


Native Multiple Network Interfaces on Pods
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Related requirements:** Virtual Network Interface
Specifications (Chapter 4 of :cite:t:`refmodel`)

**Baseline project:** *Kubernetes*

**Gap description:** Kubernetes lacks native support for
multiple Pod interfaces, requiring a CNI multiplexer (like
:cite:t:`github-multus`).  Network service implementation
(Network Policies, Ingress, Egress, Load Balancers) depends
on the multiplexer and its CNI plugins, leading to
inconsistency.

**Status:** A KEP (:cite:t:`googledocs-kep-multi-network-
pod-object`) aims to natively support multiple Pod
interfaces.


Dynamic Network Management
~~~~~~~~~~~~~~~~~~~~~~~~~~

**Related requirements:** ``inf.ntw.03``
(:ref:`chapters/chapter02:kubernetes architecture
requirements`)

**Baseline project:** *Kubernetes*

**Gap description:** Kubernetes lacks an API for network
service management (e.g., VPNs).  A CNI plugin
(:cite:t:`github-multus`) or integration with SDN
controllers (using NetConf, etc.) is needed to provide
APIs for network services and connect VPNs (e.g., L3VPN)
to CNFs on demand.


Control Plane Efficiency
~~~~~~~~~~~~~~~~~~~~~~~~

**Related requirements:** None

**Baseline project:** *Kubernetes*

**Gap description:**  Multi-site/availability zone
deployments often utilize multiple Kubernetes clusters for
security, multitenancy, fault tolerance, resilience, and
latency. This creates Kubernetes control plane node
overhead.  More efficient multi-cluster operation is
needed to meet non-functional requirements.


Interoperability with VRF-based Networking
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Related requirements:** None

**Baseline project:** *Kubernetes*

**Gap description:**  L3 VRFs/VPNs are commonly used for
traffic separation (signaling, charging, LI, O&M).  CNFs
must interoperate with existing network elements,
requiring Kubernetes Pod connection to L3 VPNs (currently
only possible via Multus).  However, network orchestration
(connecting the interface to a gateway router terminating
the L3 VPN) isn't handled by Kubernetes, and lacks a
production-grade open-source solution.

.. note:: While possible with IaaS, this creates an
          undesirable dependency between Kubernetes workload
          orchestration and IaaS infrastructure orchestration.


Hardware Topology-Aware Huge Pages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Related requirements:** ``infra.com.cfg.004`` and
``infra.com.cfg.002`` (Virtual Compute Profiles, Chapter 5
of :cite:t:`refmodel`).

**Baseline project:** *Kubernetes*

**Gap description:** The Memory Manager (alpha feature in
v1.21) is addressed in
:ref:`chapters/chapter03:management of memory and huge
pages resources`.


User Namespaces in Kubernetes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Related requirements:** ``e.man.004`` (Cloud
Infrastructure Management Capabilities, Chapter 4 of
:cite:t:`refmodel`), ``inf.ntw.03`` (Platform and Access
Requirements, Chapter 2 of :cite:t:`anuket-ra1`)

**Baseline project:** *Kubernetes*

**Gap description:** Kubernetes lacks namespace-scoped UIDs.
CNFs requiring system privileges must run in privileged
mode or use random system UIDs. Random UIDs cause errors
when setting kernel capabilities (e.g., VLAN trunking) or
sharing data via persistent storage.  Privileged mode is
insecure; random UIDs are error-prone.  Proper user
namespaces (alpha in Kubernetes 1.25
:cite:t:`kubernetes-user-namespaces`, KEP
:cite:t:`kubernetes-kep-user-namespaces`) are needed.
