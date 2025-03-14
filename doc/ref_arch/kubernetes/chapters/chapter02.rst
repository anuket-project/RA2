Architecture Requirements
=========================

Introduction for Architecture Requirements
------------------------------------------

This chapter will specialise the requirements defined in the overall Reference Model into Kubernetes-specific
requirements. Additional, RA2-specific, entries are included in section
:ref:`chapters/chapter02:kubernetes architecture requirements`.

Key Word Definitions
--------------------

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in RFC 2119 :cite:p:`rfc2119`.

Reference Model Requirements
----------------------------

The tables below contain the requirements from the Reference Model to cover all infrastructure profiles.
The table also includes a reference to any linked specification at
:ref:`chapters/chapter04:component level architecture` and at
:ref:`chapters/chapter05:security guidance` to ensure traceability. If the related Specification
does not exist, the reference will read "N/A" (and in bold "**N/A**" for mandatory requirements).

To ensure alignment with the infrastructure profile catalogue, the following requirements are referenced through:

-  Those relating to Cloud Infrastructure Software Profiles
-  Those relating to Cloud Infrastructure Hardware Profiles
-  Those relating to Cloud Infrastructure Management
-  Those relating to Cloud Infrastructure Security

Cloud Infrastructure Software Profile Capabilities
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: Reference Model Requirements: Cloud Infrastructure Software Profile Capabilities
   :widths: 10 10 50 10 10 10
   :header-rows: 1

   * - Reference Model Section :cite:p:`refmodel`
     - Reference
     - Description
     - Requirement for Basic Profile
     - Requirement for High-Performance Profile
     - Specification Reference
   * - Exposed Infrastructure Capabilities
     - e.cap.001
     - Max number of vCPU that can be assigned to a single Pod by the Cloud Infrastructure
     - At least 16
     - At least 16
     - ra2.ch.011
   * - Exposed Infrastructure Capabilities
     - e.cap.002
     - Max memory in MB that can be assigned to a single Pod by the Cloud Infrastructure
     - at least 32 GB
     - at least 32 GB
     - ra2.ch.012
   * - Exposed Infrastructure Capabilities
     - e.cap.003
     - Max storage in GB that can be assigned to a single Pod by the Cloud Infrastructure
     - at least 320 GB
     - at least 320 GB
     - ra2.ch.010
   * - Exposed Infrastructure Capabilities
     - e.cap.004
     - Max number of connection points that can be assigned to a single Pod by the Cloud Infrastructure
     - 6
     - 6
     - ra2.ntw.003
   * - Exposed Infrastructure Capabilities
     - e.cap.005
     - Max storage in GB that can be attached / mounted to Pod by the Cloud Infrastructure
     - Up to 16TB (1)
     - Up to 16TB (1)
     - N/A
   * - Profiles Specifications & Capability Mapping
     - e.cap.006
     - CPU pinning support
     - Optional
     - Must support
     - ra2.k8s.009
   * - Profiles Specifications & Capability Mapping
     - e.cap.007
     - NUMA support
     - Optional
     - Must support
     - ra2.k8s.006
   * - Exposed Infrastructure Capabilities
     - e.cap.008
     - IPsec Acceleration using the virtio-ipsec interface
     - Optional
     - Optional
     - N/A
   * - Exposed Infrastructure Capabilities
     - e.cap.009
     - Crypto Acceleration using the virtio-crypto interface
     - Optional
     - Optional
     - N/A
   * - Exposed Infrastructure Capabilities
     - e.cap.010
     - Transcoding Acceleration
     - Optional
     - Optional
     - N/A
   * - Exposed Infrastructure Capabilities
     - e.cap.011
     - Programmable Acceleration
     - Optional
     - Optional
     - N/A
   * - Exposed Infrastructure Capabilities
     - e.cap.012
     - Enhanced Cache Management: L=Lean; E=Equal; X=eXpanded
     - E
     - E
     - N/A
   * - Profiles Specifications & Capability Mapping
     - e.cap.013
     - SR-IOV over PCI-PT
     - Optional
     - Must support
     - ra2.ch.002 ra2.ch.003 ra2.k8s.007 ra2.ntw.004 ra2.ntw.008
   * - Exposed Infrastructure Capabilities
     - e.cap.014
     - Hardware coprocessor support (GPU/NPU)
     - Optional
     - Optional
     - N/A
   * - Exposed Infrastructure Capabilities
     - e.cap.015
     - SmartNICs
     - Optional
     - Optional
     - N/A
   * - Exposed Infrastructure Capabilities
     - e.cap.016
     - FPGA/other Acceleration H/W
     - Optional
     - Optional
     - ra2.k8s.007 ra2.ntw.012
   * - Exposed Infrastructure Capabilities
     - e.cap.017
     - Ability to monitor L2-L7 data from workload
     - n/a (2)
     - *n/a (2)*
     - N/A
   * - Exposed Infrastructure Capabilities
     - e.cap.026
     - Real-Time settings
     - No
     - Mandatory for flavour `rt-tsn`
     -
   * - Exposed Infrastructure Capabilities
     - e.cap.027
     - Time Sensitive Networking with PTP Hardware Clock and syncronization with SyncE
     - No
     - Mandatory for flavour `rt-tsn`
     -
   * - Internal Infrastructure Capabilities
     - i.cap.014
     - Specifies the proportion of vCPUs consumed by the Cloud Infrastructure system on the worker
       nodes.
     - 2
     - 2
     - ra2.k8s.008
   * - Internal Infrastructure Capabilities
     - i.cap.015
     - Indicates the memory consumed by Cloud Infrastructure on the worker nodes
     - 16 GB
     - 16 GB
     -
   * - Internal Infrastructure Capabilities
     - i.cap.016
     - Number of virtual cores per physical core; also known as CPU overbooking ratio that is required
     - 01:01
     - 01:01
     - ra2.ch.004, ra2.ch.005 :ref:`chapters/chapter04:kubernetes node`
   * - Internal Infrastructure Capabilities
     - i.cap.017
     - QoS enablement of the connection point (vNIC or interface)
     - Optional
     - Must support
     - N/A
   * - Internal Infrastructure Capabilities
     - i.cap.018
     - Support for huge pages
     - Optional
     - Must support
     - ra2.ch.001
   * - Internal Infrastructure Capabilities
     - i.pm.001
     - Monitor worker node CPU usage, per nanosecond
     - Must support
     - Must support
     - N/A
   * - Internal Infrastructure Capabilities
     - i.pm.002
     - Monitor Pod CPU usage, per nanosecond
     - Must support
     - Must support
     - N/A
   * - Internal Infrastructure Capabilities
     - i.pm.003
     - Monitor worker node CPU utilisation (%)
     - Must support
     - Must support
     - N/A
   * - Internal Infrastructure Capabilities
     - i.pm.004
     - Monitor Pod CPU utilisation
     - Must support
     - Must support
     - N/A
   * - Internal Infrastructure Capabilities
     - i.pm.005
     - Measure external storage IOPs
     - Must support
     - Must support
     - N/A
   * - Internal Infrastructure Capabilities
     - i.pm.006
     - Measure external storage throughput
     - Must support
     - Must support
     - N/A
   * - Internal Infrastructure Capabilities
     - i.pm.007
     - Measure external storage capacity
     - Must support
     - Must support
     - N/A
   * - Profiles Specifications & Capability Mapping
     - i.os.001
     - Host operating system must provide drivers etc. to support listed capabilities.
     - Must support
     - Must support
     - ra2.ch.004

**(1)** Defined in the ``.bronze`` configuration in RM section `Storage extensions` :cite:p:`refmodel`.

**(2)** In Kubernetes based infrastructures packet monitoring is out of the scope for the infrastructure.

Virtual Network Interface Specifications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  Note: The required number of connection points to a Pod is described in ``e.cap.004`` above. This section describes
  the required bandwidth of those connection points.

.. list-table:: Reference Model Requirements: Network Interface Specifications
   :widths: 10 30 30 10 10 10
   :header-rows: 1

   * - Reference Model Section :cite:p:`refmodel`
     - Reference
     - Description
     - Requirement for Basic Profile
     - Requirement for High-Performance Profile
     - Specification Reference
   * - Virtual Network Interface Specifications
     - n1, n2, n3, n4, n5, n6
     - 1, 2, 3, 4, 5, 6 Gbps
     - Must support
     - Must support
     - N/A
   * - Virtual Network Interface Specifications
     - n10, n20, n30, n40, n50, n60
     - 10, 20, 30, 40, 50, 60 Gbps
     - Must support
     - Must support
     - N/A
   * - Virtual Network Interface Specifications
     - n25, n50, n75, n100, n125, n150
     - 25, 50, 75, 100, 125, 150 Gbps
     - Must support
     - Must support
     - N/A
   * - Virtual Network Interface Specifications
     - n50, n100, n150, n200, n250 , n300
     - 50, 100, 150, 200, 250, 300 Gbps
     - Must support
     - Must support
     - N/A
   * - Virtual Network Interface Specifications
     - n100, n200, n300, n400, n500, n600
     - 100, 200, 300, 400, 500, 600 Gbps
     - Must support
     - Must support
     - N/A

Virtual Network Interface Specifications


Cloud Infrastructure Software Profile Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: Reference Model Requirements: Cloud Infrastructure Software Profile Requirements
   :widths: 10 10 50 10 10 10
   :header-rows: 1

   * - Reference Model Section :cite:p:`refmodel`
     - Reference
     - Description
     - Requirement for Basic Profile
     - Requirement for High-Performance Profile
     - Specification Reference
   * - Virtual Compute
     - infra.com.cfg.001
     - CPU allocation ratio
     - 1:1
     - 1:1
     - ra2.ch.005, ra2.ch.006
   * - Virtual Compute
     - infra.com.cfg.002
     - NUMA awareness
     - Optional
     - Must support
     - ra2.k8s.006
   * - Virtual Compute
     - infra.com.cfg.003
     - CPU pinning capability
     - Optional
     - Must support
     - ra2.k8s.009
   * - Virtual Compute
     - infra.com.cfg.004
     - Huge pages
     - Optional
     - Must support
     - ra2.ch.001
   * - Virtual Storage
     - infra.stg.cfg.002
     - Storage Block
     - Must support
     - Must support
     - ra2.stg.004
   * - Virtual Storage
     - infra.stg.cfg.003
     - Storage with replication
     - Must support
     - Must support
     - N/A
   * - Virtual Storage
     - infra.stg.cfg.004
     - Storage with encryption
     - Optional
     - Optional
     - N/A
   * - Virtual Storage
     - infra.stg.acc.cfg.001
     - Storage IOPS oriented encryption
     - Optional
     - Must support
     - N/A
   * - Virtual Storage
     - infra.stg.acc.cfg.002
     - Storage capacity-oriented encryption
     - Optional
     - Optional
     - N/A
   * - Virtual Networking
     - infra.net.cfg.001
     - IO virtualisation using virtio1.1
     - Must support (1)
     - Must support (1)
     - N/A
   * - Virtual Networking
     - infra.net.cfg.002
     - The overlay network encapsulation protocol needs to enable ECMP in the underlay to take advantage of the
       scale-out features of the network fabric.(2)
     - Must support VXLAN, MPLSoUDP, GENEVE, other
     - No requirement specified
     - N/A
   * - Virtual Networking
     - infra.net.cfg.003
     - Network Address Translation
     - Must support
     - Must support
     - N/A
   * - Virtual Networking
     - infra.net.cfg.004
     - Security Groups
     - Must support
     - Must support
     - ra2.k8s.014
   * - Virtual Networking
     - infra.net.cfg.006
     - Traffic patterns symmetry
     - Must support
     - Must support
     - N/A
   * - Virtual Networking
     - infra.net.acc.cfg.001
     - vSwitch optimisation
     - Optional
     - Must support DPDK (3)
     - ra2.ntw.010
   * - Virtual Networking
     - infra.net.acc.cfg.002
     - Support of HW offload
     - Optional
     - Optional, SmartNIC
     - N/A
   * - Virtual Networking
     - infra.net.acc.cfg.003
     - Crypto acceleration
     - Optional
     - Optional
     - N/A
   * - Virtual Networking
     - infra.net.acc.cfg.004
     - Crypto Acceleration Interface
     - Optional
     - Optional
     - N/A
   * - Virtual Networking
     - infra.net.acc.cfg.005
     - AF_XDP
     - Optional
     - Optional
     - N/A

Virtual Networking

**(1)** Might have other interfaces (such as SR-IOV VFs to be directly passed to a VM or a Pod) or NIC-specific drivers
on Kubernetes nodes.

**(2)** In Kubernetes based infrastructures network separation is possible without an overlay (e.g.: with IPVLAN)

**(3)** This feature is not applicable for Kubernetes based infrastructures due to lack of vSwitch however workloads
need access to user space networking solutions.

Cloud Infrastructure Hardware Profile Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: Reference Model Requirements: Cloud Infrastructure Hardware Profile Requirements
   :widths: 10 10 50 10 10 10
   :header-rows: 1

   * - Reference Model Section :cite:p:`refmodel`
     - Reference
     - Description
     - Requirement for Basic Profile
     - Requirement for High-Performance Profile
     - Specification Reference
   * - Compute Resources
     - infra.hw.cpu.cfg.001
     - Minimum number of CPU sockets
     - 2
     - 2
     - ra2.ch.008
   * - Compute Resources
     - infra.hw.cpu.cfg.002
     - Minimum number of cores per CPU
     - 20
     - 20
     - ra2.ch.008
   * - Compute Resources
     - infra.hw.cpu.cfg.003
     - NUMA alignment
     - N
     - Y
     - ra2.ch.008
   * - Compute Resources
     - infra.hw.cpu.cfg.004
     - Simultaneous multithreading/ Symmetric multiprocessing (SMT/SMP)
     - Must support if available
     - Optional
     - ra2.ch.004
   * - Compute Resources
     - infra.hw.cac.cfg.001
     - GPU
     - Optional
     - Optional
     - N/A
   * - Storage Configurations`
     - infra.hw.stg.hdd.cfg.001
     - Local storage HDD
     - No requirement specified
     - No requirement specified
     - N/A
   * - Storage Configurations`
     - infra.hw.stg.ssd.cfg.002
     - Local storage SSD
     - Should support
     - Should support
     - ra2.ch.009
   * - Network Resources
     - infra.hw.nic.cfg.001
     - Total number of NIC ports available in the host
     - 4
     - 4
     - ra2.ch.013
   * - Network Resources
     - infra.hw.nic.cfg.002
     - Port speed specified in Gbps (minimum values)
     - 10
     - 25
     - ra2.ch.014, ra2.ch.015
   * - Network Resources
     - infra.hw.pci.cfg. 001
     - Number of PCIe slots available in the host
     - 8
     - 8
     - ra2.ch.016
   * - Network Resources
     - infra.hw.pci.cfg.002
     - PCIe speed
     - Gen 3
     - Gen 3
     - ra2.ch.016
   * - Network Resources
     - infra.hw.pci.cfg.003
     - PCIe lanes
     - 8
     - 8
     - ra2.ch.016
   * - Network Resources
     - infra.hw.nac.cfg.001
     - Cryptographic acceleration
     - Optional
     - Optional
     - N/A
   * - Network Resources
     - infra.hw.nac.cfg.002
     - A SmartNIC that is used to offload vSwitch functionality to hardware
     - Optional
     - Optional (1)
     - N/A
   * - Network Resources
     - infra.hw.nac.cfg.003
     - Compression
     - Optional
     - Optional
     - N/A

**(1)** There is no vSwitch in case of containers, but a SmartNIC can be used to offload any other network processing.

Edge Cloud Infrastructure Hardware Profile Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the case of Telecom Edge Cloud Deployments, hardware requirements can differ from the above to account for
environmental and other constraints.
The Reference Model :cite:p:`refmodel`
includes considerations specific to deployments at the edge of the network. The infrastructure profiles "Basic" and
"High Performance" as per the RM chapter on `Profiles and Workload Flavours` still apply, but a number
of requirements of the above table are relaxed as follows:

.. list-table:: Reference Model Requirements: Edge Cloud Infrastructure Hardware Profile Requirements
   :widths: 10 10 50 10 10 10
   :header-rows: 1

   * - Reference Model Section :cite:p:`refmodel`
     - Reference
     - Description
     - Requirement for Basic Profile
     - Requirement for High-Performance Profile
     - Specification Reference
   * - Telecom Edge Cloud: Infrastructure Profiles
     - infra.hw.cpu.cfg.001
     - sockets
     -
     -
     -
   * - Telecom Edge Cloud: Infrastructure Profiles
     - infra.hw.cpu.cfg.002
     - Minimum number of Cores per CPU
     - 1
     - 1
     - ra2.ch.008
   * - Telecom Edge Cloud: Infrastructure Profiles
     - infra.hw.cpu.cfg.003
     - NUMA alignment
     - N
     - Y (1)
     - ra2.ch.008

Telecom Edge Cloud: Infrastructure Profiles.

**(1)** immaterial if the number of CPU sockets (infra.hw.cpu.cfg.001) is 1.

Cloud Infrastructure Management Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: Reference Model Requirements: Cloud Infrastructure Management Requirements
   :widths: 10 10 50 10 10
   :header-rows: 1

   * - Reference Model Section :cite:p:`refmodel`
     - Reference
     - Description
     - Requirement (common to all Profiles)
     - Specification Reference
   * - Cloud Infrastructure Management Capabilities
     - e.man.001
     - Capability to allocate virtual compute resources to a workload
     - Must support
     - N/A
   * - Cloud Infrastructure Management Capabilities
     - e.man.002
     - Capability to allocate virtual storage resources to a workload
     - Must support
     - N/A
   * - Cloud Infrastructure Management Capabilities
     - e.man.003
     - Capability to allocate virtual networking resources to a workload
     - Must support
     - N/A
   * - Cloud Infrastructure Management Capabilities
     - e.man.004
     - Capability to isolate resources between tenants
     - Must support
     - N/A
   * - Cloud Infrastructure Management Capabilities
     - e.man.005
     - Capability to manage workload software images
     - Must support
     - N/A
   * - Cloud Infrastructure Management Capabilities
     - e.man.006
     - Capability to provide information related to allocated virtualised resources per tenant
     - Must support
     - N/A
   * - Cloud Infrastructure Management Capabilities
     - e.man.007
     - Capability to notify state changes of allocated resources
     - Must support
     - N/A
   * - Cloud Infrastructure Management Capabilities
     - e.man.008
     - Capability to collect and expose performance information on virtualised resources allocated
     - Must support
     - N/A
   * - Cloud Infrastructure Management Capabilities
     - e.man.009
     - Capability to collect and notify fault information on virtualised resources
     - Must support
     - N/A

Cloud Infrastructure Management Capabilities.

Cloud Infrastructure Monitoring Capabilities
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: Reference Model Requirements: Cloud Infrastructure Internal Performance Measurement Requirements
   :widths: 10 10 50 10 10
   :header-rows: 1

   * - Reference Model Section :cite:p:`refmodel`
     - Reference
     - Description
     - Requirement (common to all Profiles)
     - Specification Reference
   * - Internal Performance Measurement Capabilities
     - i.pm.001
     - Capability to monitor host CPU Usage (in ns)
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.002
     - Capability to monitor per Pod CPU (Virtual compute resource) usage (in ns)
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.003
     - Capability to monitor host CPU Usage (in percentage)
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.004
     - Capability to monitor per Pod CPU (Virtual compute resource) usage (in percentage)
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.005
     - Capability to monitor packet count per physical or virtual node network interface
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.006
     - Capability to monitor octet (bytes) count per physical or virtual node network interface
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.007
     - Capability to monitor dropped packet count per physical or virtual node network interface
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.008
     - Capability to monitor errored packet count per physical or virtual node network interface
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.009
     - Capability to monitor amount of buffered memory (in KiB) on the node.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.010
     - Capability to monitor amount of cached memory (in KiB) on the node.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.011
     - Capability to monitor amount of free memory (in KiB) on the node.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.012
     - Capability to monitor amount of slab memory (in KiB) on the node.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.013
     - Capability to monitor amount of total memory (in KiB) on the node.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.014
     - Capability to monitor amount of free storage space (in B) on the node and on volumes.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.015
     - Capability to monitor amount of used storage space (in B) on the node and on volumes.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.016
     - Capability to monitor amount of reserved storage space (in B) on the node and on volumes.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.017
     - Capability to monitor the storage read latency (in ms) on the node and on volumes.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.018
     - Capability to monitor the read operations rate (in IOPS) on the node and on volumes.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.019
     - Capability to monitor the storage read throughput (in B/s) on the node and on volumes.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.020
     - Capability to monitor the storage write latency (in ms) on the node and on volumes.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.021
     - Capability to monitor the write operations rate (in IOPS) on the node and on volumes.
     - Must support
     - N/A
   * - Internal Performance Measurement Capabilities
     - i.pm.022
     - Capability to monitor the storage write throughput (in B/s) on the node and on volumes.
     - Must support
     - N/A

Internal Performance Measurement Capabilities.



Cloud Infrastructure Security Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: Reference Model Requirements: Cloud Infrastructure Security Requirements
   :widths: 10 10 70 10
   :header-rows: 1

   * - Reference Model Section :cite:p:`refmodel`
     - Reference
     - Description
     - Specification Reference
   * - System Hardening
     - sec.gen.001
     - The Platform **must** maintain the specified configuration.
     -
   * - System Hardening
     - sec.gen.002
     - All systems part of Cloud Infrastructure **must** support password hardening as defined in the
       CIS Password Policy Guide :cite:p:`cispwpolicy`.
       Hardening: CIS Password Policy Guide
     - `Node Hardening: Securing Kubernetes Hosts`
   * - System Hardening
     - sec.gen.003
     - All servers part of Cloud Infrastructure **must** support a root of trust and secure boot.
     -
   * - System Hardening
     - sec.gen.004
     - The Operating Systems of all the servers part of Cloud Infrastructure **must** be hardened by removing or
       disabling unnecessary services, applications, and network protocols, configuring operating system user
       authentication, configuring resource controls, installing and configuring additional security controls where
       needed, and testing the security of the Operating System. (NIST SP 800-123)
     - :ref:`chapters/chapter05:security principles` and :ref:`chapters/chapter05:node hardening`
   * - System Hardening
     - sec.gen.005
     - The Platform **must** support Operating System level access control
     - :ref:`chapters/chapter05:node hardening`
   * - System Hardening
     - sec.gen.006
     - The Platform **must** support secure logging. Logging with root account must be prohibited when root
       privileges are not required.
     - :ref:`chapters/chapter05:restricting direct access to nodes`
   * - System Hardening
     - sec.gen.007
     - All servers part of Cloud Infrastructure **must** be Time synchronized with authenticated Time service.
     -
   * - System Hardening
     - sec.gen.008
     - All servers part of Cloud Infrastructure **must** be regularly updated to address security vulnerabilities.
     - :ref:`chapters/chapter05:vulnerability assessment`
   * - System Hardening
     - sec.gen.009
     - The Platform **must** support Software integrity protection and verification and **must** scan source code
       and manifests.
     - :ref:`chapters/chapter05:securing the kubernetes orchestrator`
   * - System Hardening
     - sec.gen.010
     - The Cloud Infrastructure **must** support encrypted storage, for example, block, object and file storage,
       with access to encryption keys restricted based on a need to know. Controlled Access Based on the Need
       to Know :cite:p:`ciscontrolslist`.
     -
   * - System Hardening
     - sec.gen.011
     - The Cloud Infrastructure **should** support Read and Write only storage partitions (write only permission
       to one or more authorized actors).
     -
   * - System Hardening
     - sec.gen.012
     - The Operator **must** ensure that only authorized actors have physical access to the underlying infrastructure.
     -
   * - System Hardening
     - sec.gen.013
     - The Platform **must** ensure that only authorized actors have logical access to the underlying infrastructure.
     - :ref:`chapters/chapter05:securing the kubernetes orchestrator`
   * - System Hardening
     - sec.gen.014
     - All servers part of Cloud Infrastructure **should** support measured boot and an attestation server that monitors
       the measurements of the servers.
     -
   * - System Hardening
     - sec.gen.015
     - Any change to the Platform must be logged as a security event, and the logged event must include
       the identity of the entity making the change, the change, the date and the time of the change.
     -
   * - Platform and Access
     - sec.sys.001
     - The Platform **must** support authenticated and secure access to API, GUI and command line interfaces.
     - :ref:`chapters/chapter05:securing the kubernetes orchestrator`
   * - Platform and Access
     - sec.sys.002
     - The Platform **must** support Traffic Filtering for workloads (for example, Firewall).
     -
   * - Platform and Access
     - sec.sys.003
     - The Platform **must** support secure and encrypted communications, and confidentiality and integrity of
       network traffic.
     - `Network Resources Use Transport Layer Security and Service Mesh`
   * - Platform and Access
     - sec.sys.004
     - The Cloud Infrastructure **must** support authentication, integrity, and confidentiality on all network
       channels.
     - `Network Resources Use Transport Layer Security and Service Mesh`
   * - Platform and Access
     - sec.sys.005
     - The Cloud Infrastructure **must** separate the underlay and overlay networks.
     -
   * - Platform and Access
     - sec.sys.006
     - The Cloud Infrastructure must be able to utilise the Cloud Infrastructure Manager identity lifecycle
       management capabilities.
     - :ref:`chapters/chapter05:security principles`
   * - Platform and Access
     - sec.sys.007
     - The Platform **must** implement controls enforcing separation of duties and privileges, least privilege
       use and least common mechanism (Role-Based Access Control).
     - :ref:`chapters/chapter05:security principles` :ref:`chapters/chapter05:securing the kubernetes orchestrator`
   * - Platform and Access
     - sec.sys.008
     - The Platform **must** be able to assign the Entities that comprise the tenant networks to different
       trust domains. Communication between different trust domains is not allowed, by default.
     -
   * - Platform and Access
     - sec.sys.009
     - The Platform **must** support creation of Trust Relationships between trust domains.
     -
   * - Platform and Access
     - sec.sys.010
     - For two or more domains without existing trust relationships, the Platform **must not** allow the effect
       of an attack on one domain to impact the other domains either directly or indirectly.
     -
   * - Platform and Access
     - sec.sys.011
     - The Platform **must not** reuse the same authentication credential (e.g., key-pair) on different Platform
       components (e.g., on different hosts, or different services).
     -
   * - Platform and Access
     - sec.sys.012
     - The Platform **must** protect all secrets by using strong encryption techniques, and storing the protected
       secrets externally from the component
     -
   * - Platform and Access
     - sec.sys.013
     - The Platform **must** provide secrets dynamically as and when needed.
     -
   * - Platform and Access
     - sec.sys.014
     - The Platform **should** use Linux Security Modules such as SELinux to control access to resources.
     -
   * - Platform and Access
     - sec.sys.015
     - The Platform **must not** contain back door entries (unpublished access points, APIs, etc.).
     -
   * - Platform and Access
     - sec.sys.016
     - Login access to the platform's components **must** be through encrypted protocols such as SSH v2
       or TLS v1.2 or higher. Note: Hardened jump servers isolated from external networks are recommended
     - :ref:`chapters/chapter05:securing the kubernetes orchestrator`
   * - Platform and Access
     - sec.sys.017
     - The Platform **must** provide the capability of using digital certificates that comply with X.509 standards
       issued by a trusted certificate authority.
     -
   * - Platform and Access
     - sec.sys.018
     - The Platform **must** provide the capability of allowing certificate renewal and revocation.
     -
   * - Platform and Access
     - sec.sys.019
     - The Platform **must** provide the capability of testing the validity of a digital certificate (CA signature,
       validity period, non-revocation, identity).
     -
   * - Platform and Access
     - sec.sys.020
     - The Cloud Infrastructure architecture **should** rely on Zero Trust principles to build a secure by design
       environment.
     -
   * - Confidentiality and Integrity
     - sec.ci.001
     - The Platform **must** support Confidentiality and Integrity of data at rest and in-transit. by design
       environment.
     - :ref:`chapters/chapter05:securing the kubernetes orchestrator`
   * - Confidentiality and Integrity
     - sec.ci.002
     - The Platform **should** support self-encrypting storage devices.
     -
   * - Confidentiality and Integrity
     - sec.ci.003
     - The Platform **must** support confidentiality and integrity of data related metadata.
     -
   * - Confidentiality and Integrity
     - sec.ci.004
     - The Platform **must** support confidentiality of processes and restrict information sharing with only the process
       owner (e.g., tenant).
     -
   * - Confidentiality and Integrity
     - sec.ci.005
     - The Platform **must** support confidentiality and integrity of process-related metadata and restrict information
       sharing with only the process owner (e.g., tenant).
     -
   * - Confidentiality and Integrity
     - sec.ci.006
     - The Platform **must** support confidentiality and integrity of workload resource utilization (RAM, CPU,
       storage, network I/O, cache, hardware offload) and restrict information sharing with only the workload
       owner (e.g., tenant).
     -
   * - Confidentiality and Integrity
     - sec.ci.007
     - The Platform **must not** allow memory inspection by any actor other than the authorized actors for the
       entity to which memory is assigned (e.g., tenants owning the workload), for Lawful Inspection, and by
       secure monitoring services.
     -
   * - Confidentiality and Integrity
     - sec.ci.008
     - The Cloud Infrastructure **must** support tenant networks segregation.
     - Create and define Network Policies
   * - Confidentiality and Integrity
     - sec.ci.009
     - For sensitive data encryption, the key management service **should** leverage a Hardware Security Module
       to manage and protect cryptographic keys.
     -
   * - Workload Security
     - sec.wl.001
     - The Platform **must** support workload placement policy.
     -
   * - Workload Security
     - sec.wl.002
     - The Cloud Infrastructure **must** provide methods to ensure the platform's trust status and integrity
       (e.g., remote attestation, Trusted Platform Module).
     -
   * - Workload Security
     - sec.wl.003
     - The Platform **must** support secure provisioning of workloads.
     - :ref:`chapters/chapter05:securing the kubernetes orchestrator`
   * - Workload Security
     - sec.wl.004
     - The Platform **must** support location assertion (for mandated in-country or location requirements).
     -
   * - Workload Security
     - sec.wl.005
     - The Platform **must** support the separation of production and non-production Workloads.
     - :ref:`chapters/chapter05:securing the kubernetes orchestrator`
   * - Workload Security
     - sec.wl.006
     - The Platform **must** support the separation of Workloads based on their categorisation (for example,
       payment card information, healthcare, etc.).
     - :ref:`chapters/chapter05:securing the kubernetes orchestrator`
   * - Workload Security
     - sec.wl.007
     - The Operator **must** implement processes and tools to verify VNF authenticity and integrity.
     - :ref:`chapters/chapter05:trusted registry`
   * - Image Security
     - sec.img.001
     - Images from untrusted sources **must not** be used.
     - :ref:`chapters/chapter05:trusted registry`
   * - Image Security
     - sec.img.002
     - Images **must** be scanned to be maintained free from known vulnerabilities.
     - :ref:`chapters/chapter05:trusted registry`
   * - Image Security
     - sec.img.003
     - Images **must not** be configured to run with privileges higher than the privileges of the actor
       authorized to run them.
     - :ref:`chapters/chapter05:runtime security`
   * - Image Security
     - sec.img.004
     - Images **must** only be accessible to authorised actors.
     -
   * - Image Security
     - sec.img.005
     - Image Registries **must** only be accessible to authorised actors.
     -
   * - Image Security
     - sec.img.006
     - Image Registries **must** only be accessible over secure networks that enforce authentication,
       integrity and confidentiality.
     - :ref:`chapters/chapter05:trusted registry`
   * - Image Security
     - sec.img.007
     - Image registries **must** be clear of vulnerable and out of date versions.
     - :ref:`chapters/chapter05:trusted registry`
   * - Image Security
     - sec.img.008
     - Images **must not** include any secrets. Secrets include passwords, cloud provider credentials,
       SSH keys, TLS certificate keys, etc.
     - :ref:`chapters/chapter05:secrets management`
   * - Image Security
     - sec.img.009
     - CIS Hardened Images **should** be used whenever possible.
     -
   * - Image Security
     - sec.img.010
     - Minimalist base images **should** be used whenever possible.
     -
   * - Security LCM
     - sec.lcm.001
     - The Platform **must** support secure provisioning, availability, and deprovisioning (secure clean-Up)
       of workload resources where secure clean-Up includes tear-down, defense against virus or other attacks.
     -
   * - Security LCM
     - sec.lcm.002
     - Cloud operations staff and systems **must** use management protocols limiting security risk such as
       SNMPv3, SSH v2, ICMP, NTP, syslog and TLS v1.2 or higher.
     - :ref:`chapters/chapter05:securing the kubernetes orchestrator`
   * - Security LCM
     - sec.lcm.003
     - The Cloud Operator **must** implement and strictly follow change management processes for Cloud
       Infrastructure, Cloud Infrastructure Manager and other components of the cloud, and platform change
       control on hardware.
     -
   * - Security LCM
     - sec.lcm.004
     - The Cloud Operator **should** support automated templated approved changes.
     -
   * - Security LCM
     - sec.lcm.005
     - Platform **must** provide logs and these logs must be regularly monitored for anomalous behavior.
     - :ref:`chapters/chapter05:enabling logging and monitoring`
   * - Security LCM
     - sec.lcm.006
     - The Platform **must** verify the integrity of all Resource management requests.
     -
   * - Security LCM
     - sec.lcm.007
     - The Platform **must** be able to update newly instantiated, suspended, hibernated, migrated and
       restarted images with current time information.
     - :ref:`chapters/chapter05:securing the kubernetes orchestrator`
   * - Security LCM
     - sec.lcm.008
     - The Platform **must** be able to update newly instantiated, suspended, hibernated, migrated and
       restarted images with relevant DNS information.
     -
   * - Security LCM
     - sec.lcm.009
     - The Platform **must** be able to update the tag of newly instantiated, suspended, hibernated,
       migrated and restarted images with relevant geolocation (geographic) information.
     -
   * - Security LCM
     - sec.lcm.010
     - The Platform **must** log all changes to geolocation along with the mechanisms and sources of
       location information (i.e., GPS, IP block, and timing).
     -
   * - Security LCM
     - sec.lcm.011
     - The Platform **must** implement security life cycle management processes including the proactive
       update and patching of all deployed Cloud Infrastructure software.
     -
   * - Security LCM
     - sec.lcm.012
     - The Platform **must** log any access privilege escalation.
     -
   * - Monitoring and Security Audit
     - sec.mon.001
     - The Platform **must** provide logs and these logs must be regularly monitored for events of interest.
       The logs **must** contain the following fields: event type, date/time, protocol, service or program
       used for access, success/failure, login ID or process ID, IP address and ports (source and destination)
       involved.
     -
   * - Monitoring and Security Audit
     - sec.mon.002
     - Security logs **must** be time synchronised.
     -
   * - Monitoring and Security Audit
     - sec.mon.003
     - The Platform **must** log all changes to time server source, time, date and time zones.
     -
   * - Monitoring and Security Audit
     - sec.mon.004
     - The Platform **must** secure and protect audit logs (containing sensitive information) both in-transit
       and at rest.
     -
   * - Monitoring and Security Audit
     - sec.mon.005
     - The Platform **must** monitor and audit various behaviours of connection and login attempts to
       detect access attacks and potential access attempts and take corrective actions accordingly.
     -
   * - Monitoring and Security Audit
     - sec.mon.006
     - The Platform **must** monitor and audit operations by authorized account access after login to
       detect malicious operational activity and take corrective actions accordingly.
     -
   * - Monitoring and Security Audit
     - sec.mon.007
     - The Platform **must** monitor and audit security parameter configurations for compliance with
       defined security policies.
     -
   * - Monitoring and Security Audit
     - sec.mon.008
     - The Platform **must** monitor and audit externally exposed interfaces for illegal access (attacks)
       and take corrective security hardening measures.
     -
   * - Monitoring and Security Audit
     - sec.mon.009
     - The Platform **must** monitor and audit service handling for various attacks (malformed messages,
       signalling flooding and replaying, etc.) and take corrective actions accordingly.
     -
   * - Monitoring and Security Audit
     - sec.mon.010
     - The Platform **must** monitor and audit running processes to detect unexpected or unauthorized
       processes and take corrective actions accordingly.
     -
   * - Monitoring and Security Audit
     - sec.mon.011
     - The Platform **must** monitor and audit logs from infrastructure elements and workloads to
       detected anomalies in the system components and take corrective actions accordingly.
     -
   * - Monitoring and Security Audit
     - sec.mon.012
     - The Platform **must** monitor and audit traffic patterns and volumes to prevent malware
       download attempts.
     -
   * - Monitoring and Security Audit
     - sec.mon.013
     - The monitoring system **must not** affect the security (integrity and confidentiality) of
       the infrastructure, workloads, or the user data (through back door entries).
     -
   * - Monitoring and Security Audit
     - sec.mon.014
     - The Monitoring systems **should not** impact IAAS, PAAS, and SAAS SLAs including availability SLAs.
     -
   * - Monitoring and Security Audit
     - sec.mon.015
     - The Platform **must** ensure that the monitoring systems are never starved of resources and **must**
       activate alarms when resource utilisation exceeds a configurable threshold.
     -
   * - Monitoring and Security Audit
     - sec.mon.016
     - The Platform Monitoring components **should** follow security best practices for auditing,
       including secure logging and tracing.
     -
   * - Monitoring and Security Audit
     - sec.mon.017
     - The Platform **must** audit systems for any missing security patches and take appropriate actions.
     - :ref:`chapters/chapter05:vulnerability assessment`
   * - Monitoring and Security Audit
     - sec.mon.018
     - The Platform, starting from initialization, **must** collect and analyze logs to identify security
       events, and store these events in an external system.
     - :ref:`chapters/chapter05:patch management`
   * - Monitoring and Security Audit
     - sec.mon.019
     - The Platform's components **must not** include an authentication credential, e.g., password, in any
       logs, even if encrypted.
     -
   * - Monitoring and Security Audit
     - sec.mon.020
     - The Platform's logging system **must** support the storage of security audit logs for a configurable
       period of time.
     -
   * - Monitoring and Security Audit
     - sec.mon.021
     - The Platform **must** store security events locally if the external logging system is unavailable and
       shall periodically attempt to send these to the external logging system until successful.
     -
   * - Open Source Software
     - sec.oss.001
     - Open source code **must** be inspected by tools with various capabilities for static and dynamic code analysis.
     - :ref:`chapters/chapter05:vulnerability assessment`
   * - Open Source Software
     - sec.oss.002
     - The CVE (Common Vulnerabilities and Exposures) :cite:p:`cve` **must** be used to identify
       vulnerabilities and their severity rating for open source code part of Cloud Infrastructure and workloads
       software.
     -
   * - Open Source Software
     - sec.oss.003
     - Critical and high severity rated vulnerabilities **must** be fixed in a timely manner. Refer to the
       CVSS (Common Vulnerability Scoring System) :cite:p:`cve` to know a vulnerability
       score and its associated rate (low, medium, high, or critical).
     -
   * - Open Source Software
     - sec.oss.004
     - A dedicated internal isolated repository separated from the production environment **must** be used to
       store vetted open source content.
     - :ref:`chapters/chapter05:trusted registry`
   * - Open Source Software
     - sec.oss.005
     - A Software Bill of Materials (`SBOM` :cite:p:`sbom`) **should** be provided or
       build, and maintained to identify the software components and their origins.
     -
   * - IaaC - Secure Design and Architecture Stage Requirements
     - sec.arch.001
     - Threat Modelling methodologies and tools **should** be used during the Secure Design and Architecture
       stage triggered by Software Feature Design trigger. It may be done manually or using tools like open source
       OWASP Threat Dragon.
     -
   * - IaaC - Secure Design and Architecture Stage Requirements
     - sec.arch.002
     - Security Control Baseline Assessment **should** be performed during the Secure Design and Architecture
       stage triggered by Software Feature Design trigger. Typically done manually by internal or independent
       assessors.
     -
   * - IaaC - Secure Code Stage Requirements
     - sec.code.001
     - Static Application Security Testing (SAST) **must** be applied during Secure Coding stage triggered by Pull,
       Clone or Comment trigger. Security testing that analyses application source code for software vulnerabilities
       and gaps against best practices. Example: open source OWASP range of tools.
     -
   * - IaaC - Secure Code Stage Requirements
     - sec.code.002
     - Software Composition Analysis (SCA) **should** be applied during Secure Coding stage triggered by Pull,
       Clone or Comment trigger. Security testing that analyses application source code or compiled code for
       software components with known vulnerabilities. Example: open source OWASP range of tools.
     -
   * - IaaC - Secure Code Stage Requirements
     - sec.code.003
     - Source Code Review **should** be performed continuously during Secure Coding stage. Typically done manually.
     -
   * - IaaC - Secure Code Stage Requirements
     - sec.code.004
     - Integrated SAST via IDE Plugins **should** be used during Secure Coding stage triggered by Developer Code
       trigger. On the local machine: through the IDE or integrated test suites; triggered on completion of coding be
       developer.
     -
   * - IaaC - Secure Code Stage Requirements
     - sec.code.005
     - SAST of Source Code Repository **should** be performed during Secure Coding stage triggered by Developer Code
       trigger. Continuous delivery pre-deployment: scanning prior to deployment.
     -
   * - IaaC - Continuous Build, Integration and Testing Stage Requirements
     - sec.bld.001
     - Static Application Security Testing (SAST) **should** be applied during the Continuous Build, Integration and
       Testing stage triggered by Build and Integrate trigger. Example: open source OWASP range of tools.
     -
   * - IaaC - Continuous Build, Integration and Testing Stage Requirements
     - sec.bld.002
     - SCA - Software Composition Analysis **should** be applied during the Continuous Build, Integration and
       Testing stage triggered by Build and Integrate trigger. Example: open source OWASP range of tools.
     -
   * - IaaC - Continuous Build, Integration and Testing Stage Requirements
     - sec.bld.003
     - Image Scan **must** be applied during the Continuous Build, Integration and Testing stage triggered by
       Package trigger. Example: A push of a container image to a container registry may trigger a vulnerability
       scan before the image becomes available in the registry.
     -
   * - IaaC - Continuous Build, Integration and Testing Stage Requirements
     - sec.bld.004
     - Dynamic Application Security Testing (DAST) **should** be applied during the Continuous Build, Integration
       and Testing stage triggered by Stage & Test trigger. Security testing that analyses a running application by
       exercising application functionality and detecting vulnerabilities based on application behaviour and response.
       Example: OWASP ZAP.
     -
   * - IaaC - Continuous Build, Integration and Testing Stage Requirements
     - sec.bld.005
     - Fuzzing **should** be applied during the Continuous Build, Integration and testing stage triggered by
       Stage & Test trigger. Fuzzing or fuzz testing is an automated software testing technique that involves
       providing invalid, unexpected, or random data as inputs to a computer program. Example: GitLab Open
       Sources Protocol Fuzzer Community Edition.
     -
   * - IaaC - Continuous Build, Integration and Testing Stage Requirements
     - sec.bld.006
     - Interactive Application Security Testing (IAST) **should** be applied during the Continuous Build, Integration
       and Testing stage triggered by Stage & Test trigger. Software component deployed with an application that
       assesses application behaviour and detects presence of vulnerabilities on an application being exercised in
       realistic testing scenarios. Example: Contrast Community Edition.
     -
   * - IaaC - Continuous Delivery and Deployment Stage Requirements
     - sec.del.001
     - Image Scan **must** be applied during the Continuous Delivery and Deployment stage triggered by
       Publish to Artifact and Image Repository trigger. Example: GitLab uses the open source Clair engine for
       container image scanning.
     -
   * - IaaC - Continuous Delivery and Deployment Stage Requirements
     - sec.del.002
     - Code Signing **must** be applied during the Continuous Delivery and Deployment stage triggered by
       Publish to Artifact and Image Repository trigger. Code Signing provides authentication to assure that
       downloaded files are from the publisher named on the certificate.
     -
   * - IaaC - Continuous Delivery and Deployment Stage Requirements
     - sec.del.003
     - Artifact and Image Repository Scan **should** be continuously applied during the Continuous Delivery
       and Deployment stage. Example: GitLab uses the open source Clair engine for container scanning.
     -
   * - IaaC - Continuous Delivery and Deployment Stage Requirements
     - sec.del.004
     - Component Vulnerability Scan **must** be applied during the Continuous Delivery and Deployment stage
       triggered by Instantiate Infrastructure trigger. The vulnerability scanning system is deployed on the cloud
       platform to detect security vulnerabilities of specified components through scanning and to provide timely
       security protection. Example: OWASP Zed Attack Proxy (ZAP).
     -
   * - IaaC - Runtime Defence and Monitoring Requirements
     - sec.run.001
     - Component Vulnerability Monitoring **must** be continuously applied during the Runtime Defence and
       Monitoring stage and remediation actions **must** be applied for high severity rated vulnerabilities.
       Security technology that monitors components like virtual servers and assesses data, applications, and
       infrastructure for security risks.
     -
   * - IaaC - Runtime Defence and Monitoring Requirements
     - sec.run.002
     - Runtime Application Self-Protection (RASP) **should** be continuously applied during the Runtime Defence
       and Monitoring stage. Security technology deployed within the target application in production for detecting,
       alerting, and blocking attacks.
     -
   * - IaaC - Runtime Defence and Monitoring Requirements
     - sec.run.003
     - Application testing and Fuzzing **should** be continuously applied during the Runtime Defence
       and Monitoring stage. Fuzzing or fuzz testing is an automated software testing technique that
       involves providing invalid, unexpected, or random data as inputs to a computer program.
       Example: GitLab Open Sources Protocol Fuzzer Community Edition.
     -
   * - IaaC - Runtime Defence and Monitoring Requirements
     - sec.run.004
     - Penetration Testing **should** be continuously applied during the Runtime Defence and Monitoring stage.
       Typically done manually.
     -
   * - Compliance With Standards
     - sec.std.001
     - The Cloud Operator **should** comply with Center for Internet Security CIS Controls :cite:p:`ciscontrolslist`.
     -
   * - Compliance With Standards
     - sec.std.002
     - The Cloud Operator, Platform and Workloads **should** follow the guidance in the CSA Security
       Guidance for Critical Areas of Focus in Cloud Computing (latest version) :cite:p:`cloudsecurityalliance`.
     -
   * - Compliance With Standards
     - sec.std.003
     - The Platform and Workloads **should** follow the guidance in the
       OWASP Cheat Sheet Series (OCSS) :cite:p:`ocss`.
     -
   * - Compliance With Standards
     - sec.std.004
     - The Cloud Operator, Platform and Workloads **should** ensure that their code is not vulnerable to the
       OWASP Top Ten Security Risks :cite:p:`owasptopten`.
     -
   * - Compliance With Standards
     - sec.std.005
     - The Cloud Operator, Platform and Workloads **should** strive to improve their maturity on the
       OWASP Software Maturity Model (SAMM) :cite:p:`owaspsamm`.
     -
   * - Compliance With Standards
     - sec.std.006
     - The Cloud Operator, Platform and Workloads **should** utilize the
       OWASP Web Security Testing Guide :cite:p:`owaspwstg`.
     -
   * - Compliance With Standards
     - sec.std.007
     - The Cloud Operator, and Platform **should** satisfy the requirements for Information Management Systems
       specified in ISO/IEC 27001 :cite:p:`isoiec27001`. ISO/IEC
       27002:2013 - ISO/IEC 27001 is the international Standard for best-practice information security management
       systems (ISMSs).
     -
   * - Compliance With Standards
     - sec.std.008
     - The Cloud Operator, and Platform **should** implement the Code of practice for Security Controls specified in
       ISO/IEC 27002:2013 (or latest) :cite:p:`isoiec27001`.
     -
   * - Compliance With Standards
     - sec.std.009
     - The Cloud Operator, and Platform **should** implement the ISO/IEC 27032:2012 (or latest)
       :cite:p:`isoiec27032` Guidelines for Cybersecurity techniques.
       ISO/IEC 27032 - ISO/IEC 27032 is the international Standard focusing explicitly on cybersecurity.
     -
   * - Compliance With Standards
     - sec.std.010
     - The Cloud Operator **should** conform to the ISO/IEC 27035 standard for incidence management.
       ISO/IEC 27035 - ISO/IEC 27035 is the international Standard for incident management.
     -
   * - Compliance With Standards
     - sec.std.011
     - The Cloud Operator **should** conform to the ISO/IEC 27031 standard for business continuity. ISO/IEC 27031 -
       ISO/IEC 27031 is the international Standard for ICT readiness for business continuity.
     -
   * - Compliance With Standards
     - sec.std.012
     - The Public Cloud Operator **must**, and the Private Cloud Operator **may** be certified to be compliant
       with the International Standard on Awareness Engagements (ISAE) 3402 (in the US: SSAE 16). International
       Standard on Awareness Engagements (ISAE) 3402. US Equivalent: SSAE16.
     -

Kubernetes Architecture Requirements
------------------------------------

The requirements in this section are to be delivered in addition to those in section `Reference Model
Requirements <#reference-model-requirements>`_, and have been
created to support the Principles defined in the first chapter :ref:`chapters/chapter01:overview` of this
Reference Architecture.

The Reference Model (RM) defines the Cloud Infrastructure, which consists of the physical resources, virtualised
resources and a software management system.

In virtualisation platforms, the Cloud Infrastructure consists of the guest operating system, hypervisor and, if
needed, other software such as libvirt. The Cloud Infrastructure Management component is responsible for, among others,
tenant management, resources management, inventory, scheduling, and access management.

With regards to containerisation platforms, the scope of the following Architecture requirements include the Cloud
Infrastructure Hardware (e.g. physical resources), Cloud Infrastructure Software (e.g. Hypervisor (optional), Container
Runtime, virtual or container Orchestrator(s), Operating System), and infrastructure resources consumed by virtual
machines or containers.

.. list-table:: Kubernetes Architecture Requirements
   :widths: 10 10 10 50 20
   :header-rows: 1

   * - Reference
     - Category
     - Sub-category
     - Description
     - Specification Reference
   * - gen.cnt.02
     - General
     - Cloud nativeness
     - The Architecture must support immutable infrastructure.
     - ra2.ch.017
   * - gen.cnt.03
     - General
     - Cloud nativeness
     - The Architecture must run conformant Kubernetes as defined by the
       CNCF :cite:p:`k8s-conformance`.
     - ra2.k8s.001
   * - gen.cnt.04
     - General
     - Cloud nativeness
     - The Architecture must support clearly defined abstraction layers - from the hardware
       infrastructure (supporting the platform) to the containerisation platform (the main concern of this
       Architecture) to the applications (workloads running on the platform).
     -
   * - gen.cnt.05
     - General
     - Cloud nativeness
     - The Architecture should support configuration of all components in an automated manner
       using openly published API definitions.
     -
   * - gen.scl.01
     - General
     - Scalability
     - The Architecture should support policy driven horizontal auto-scaling of workloads.
     -
   * - gen.rsl.01
     - General
     - Resiliency
     - The Architecture must support resilient Kubernetes components that are required for the
       continued availability of running workloads.
     - ra2.k8s.004
   * - gen.rsl.02
     - General
     - Resiliency
     - The Architecture should support resilient Kubernetes service components that are not
       subject to gen.rsl.01.
     - ra2.k8s.002, ra2.k8s.003
   * - gen.avl.01
     - General
     - Availability
     - The Architecture must provide High Availability for Kubernetes components.
     - ra2.k8s.002, ra2.k8s.003, ra2.k8s.004
   * - gen.ost.01
     - Openness
     - Availability
     - The Architecture should embrace open-based standards and technologies.
     - ra2.crt.001, ra2.crt.002, ra2.ntw.002, ra2.ntw.006, ra2.ntw.007
   * - inf.com.01
     - Infrastructure
     - Compute
     - The Architecture must provide compute resources for Pods.
     - ra2.k8s.004
   * - inf.stg.01
     - Infrastructure
     - Storage
     - The Architecture must support the ability for an operator to choose whether or
       not to deploy persistent storage for Pods.
     - ra2.stg.004
   * - inf.stg.02
     - Infrastructure
     - Storage
     - The Architecture should support multiple storage classes (e.g. Block, File).
     -
   * - inf.stg.03
     - Infrastructure
     - Storage
     - The physical machines on which the Kubernetes nodes run should be equipped with solid-state drives (SSDs).
     - ra2.ch.009
   * - inf.ntw.01
     - Infrastructure
     - Network
     - The Architecture must support network resiliency on the Kubernetes nodes.
     -
   * - inf.ntw.02
     - Infrastructure
     - Network
     - The Architecture must support redundant network connectivity to the Kubernetes
       nodes. At least two physical network connections are required for each physical Kubernetes node.
       For virtualized Kubernetes nodes, redundant network interfaces backed by redundant physical
       connections, are required on each virtualised Kubernetes node.
     -
   * - inf.ntw.03
     - Infrastructure
     - Network
     - The networking solution should be able to be centrally administered and configured.
     - ra2.ntw.001, ra2.ntw.004
   * - inf.ntw.04
     - Infrastructure
     - Network
     - The Architecture must support dual stack IPv4 and IPv6 for Kubernetes workloads.
     - ra2.ch.007, ra2.k8s.010
   * - inf.ntw.05
     - Infrastructure
     - Network
     - The Architecture must support capabilities for integrating SDN controllers.
     -
   * - inf.ntw.06
     - Infrastructure
     - Network
     - The Architecture must support more than one networking solution.
     - ra2.ntw.005, ra2.ntw.007
   * - inf.ntw.07
     - Infrastructure
     - Network
     - The Architecture must support the ability for an operator to choose whether or not
       to deploy more than one networking solution.
     - ra2.ntw.005
   * - inf.ntw.08
     - Infrastructure
     - Network
     - The Architecture must provide a default network which implements the Kubernetes network model.
     - ra2.ntw.002
   * - inf.ntw.09
     - Infrastructure
     - Network
     - The networking solution must not interfere with or cause interference to any interface or
       network it does not own.
     -
   * - inf.ntw.10
     - Infrastructure
     - Network
     - The Architecture must support Cluster wide coordination of IP address assignment.
     -
   * - inf.ntw.13
     - Infrastructure
     - Network
     - The platform must allow specifying multiple separate IP pools. Tenants are required to
       select at least one IP pool that is different from the control infrastructure IP pool or
       other tenant IP pools.
     -
   * - inf.ntw.14
     - Infrastructure
     - Network
     - The platform must allow NAT-less traffic (i.e., exposing the Pod IP address directly to the
       outside), allowing source and destination IP addresses to be preserved in the traffic headers
       from workloads to external networks. This is needed e.g. for signalling applications, using SIP
       and Diameter protocols.
     - ra2.ntw.011
   * - inf.ntw.15
     - Infrastructure
     - Network
     - The platform must support LoadBalancer Publishing Service (ServiceType)
     -
   * - inf.ntw.16
     - Infrastructure
     - Network
     - The platform must support Ingress.
     -
   * - inf.ntw.17
     - Infrastructure
     - Network
     - The platform should support NodePort Publishing Service (ServiceTypes).
     -
   * - inf.ntw.18
     - Infrastructure
     - Network
     - The platform should support ExternalName Publishing Service (ServiceTypes).
     -
   * - inf.vir.01
     - Infrastructure
     - Virtual Infrastructure
     - The Architecture must support the capability for containers to consume infrastructure resources
       abstracted by host operating systems that are running within a virtual machine.
     - ra2.ch.005, ra2.ch.011
   * - inf.phy.01
     - Infrastructure
     - Physical Infrastructure
     - The Architecture must support the capability for containers to consume infrastructure resources
       abstracted by host operating systems that are running within a physical server.
     - ra2.ch.008
   * - kcm.gen.01
     - Kubernetes Cluster
     - General
     - The Architecture must support policy driven horizontal auto- scaling of Kubernetes cluster.
     - N/A
   * - kcm.gen.02
     - Kubernetes Cluster
     - General
     - The Architecture must enable workload resiliency.
     - ra2.k8s.004
   * - kcm.gen.03
     - Kubernetes Cluster
     - General
     - The Architecture should enable automated TLS certificate management.
     - ra2.k8s.020
   * - int.api.01
     - API
     - General
     - The Architecture must leverage the Kubernetes APIs to discover and declaratively manage compute
       (virtual and bare metal resources), network, and storage.
     - For Networking: ra2.ntw.001, ra2.ntw.008, ra2.app.006. Compute/storage not yet met.
   * - int.api.02
     - API
     - General
     - The Architecture must support the usage of a Kubernetes application package manager using the
       Kubernetes API, like Helm v3.
     - ra2.pkg.001
   * - int.api.03
     - API
     - General
     - The Architecture must support stable features in its APIs.
     -
   * - int.api.04
     - API
     - General
     - The Architecture must support limited backward compatibility in its APIs. Support for the whole
       API must not be dropped, but the schema or other details can change.
     -
