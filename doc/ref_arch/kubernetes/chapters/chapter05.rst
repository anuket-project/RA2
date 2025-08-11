Security Guidance
=================

Introduction to Security Guidance
---------------------------------

Securing Kubernetes requires a multi-layered security approach to protect cloud-native applications. The following best
practices are recommended:

- Security testing should be fully integrated into the CI/CD pipelines of all stakeholders (e.g., vendors and
  operators).
- Automated security policies should flag builds with identified issues.
- Image registries should be monitored to automatically block or replace images with known vulnerabilities. Policies
  should also govern what can be deployed and who can deploy from the registry.
- A layered packaging model should be adopted to support separation of concerns during image builds.

The following functionalities are recommended for securing Kubernetes platforms:

- Image certification (vulnerability scanning) and signing.
- Role-Based Access Control (RBAC).
- Secret management.
- Addressing the limitations of hard Kubernetes cluster multitenancy:

   - For tenants without strict multitenancy requirements (such as multiple development teams within the same
     organization), namespaces can provide sufficient separation.
   - For strict multitenancy, a dedicated Kubernetes cluster per tenant is recommended.

- Integration with other security tools, such as monitoring and alerting systems.

Security Perimeters
~~~~~~~~~~~~~~~~~~~

Securing applications and workloads on Kubernetes involves securing several layers. Each layer requires its own
perimeter security:

- **Container Registry:** The container registry stores and manages container images. Access must be secured to prevent
  unauthorized access and image tampering.
- **Container Images:** Container images are lightweight, portable executables containing software and dependencies.
  Before uploading to a registry, images should undergo security checks, including vulnerability analysis and scans.
  Images should also be signed by trusted sources.
- **Containers:** A container is a running instance of a container image. Containers should be prevented from accessing
  underlying OS capabilities (e.g., loading kernel modules, mounting OS directories) and should not run in privileged
  mode.
- **Pods:** A pod represents a set of running containers in a Kubernetes cluster. Kubernetes' Pod Security Policies
  define conditions for pod execution, ensuring necessary checks are performed.
- **Kubernetes Node (Worker Node):** A Kubernetes node (worker node) is a physical or virtual server running workloads.
  Unsecured nodes pose a significant threat. Nodes should be hardened by disabling unused ports, prohibiting root
  access, etc.
- **Kubernetes Control Plane Node:** An unsecured control plane node presents a significant threat. These nodes should
  be hardened by disabling unused ports, prohibiting root access, etc.
- **Kubernetes Control Plane:** The Kubernetes control plane orchestrates containers, exposing APIs and interfaces for
  managing their lifecycle. API communication should be secured using mechanisms such as TLS encryption and API
  authentication (e.g., via LDAP).

Security Principles
-------------------

Core principles for securing cloud-native applications include:

- Deploy only secure and trusted applications and code.
- Deploy applications only from validated and verified images.
- Deploy applications only from trusted registries.
- Secure Kubernetes container orchestration with administrative boundaries between tenants:

   - Use Namespaces to establish security boundaries between tenants.
   - Create and define cluster Network Policies.
   - Implement cluster-wide pod security policies.
   - Enable audit logging.
   - Isolate sensitive workloads using Namespaces.
   - Secure tenant metadata access.

- Segment container networks using security zoning and network standards.
- Harden the host OS running the containers.
- Use container-aware runtime defense tools.
- Enable Role-Based Access Control (RBAC).

Node Hardening
--------------

Node Hardening: Securing the Kubernetes Hosts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Operating systems and applications often have insecure default settings (open ports, enabled services). Kubernetes
nodes must be secured, hardened, and correctly configured according to established security frameworks (e.g., CIS
benchmarks). These benchmarks provide configuration standards and best practices for hardening digital assets.

Restricting Direct Access to Nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Restrict root/administrative access to Kubernetes nodes and avoid direct access for operational tasks (debugging,
troubleshooting, etc.).

Vulnerability Assessment
~~~~~~~~~~~~~~~~~~~~~~~~

Regular vulnerability assessments are crucial for IT risk management. Implement vulnerability scanner tools (e.g.,
OpenVAS, or other open source or commercial tools) to identify and mitigate threats and vulnerabilities.

Patch Management
~~~~~~~~~~~~~~~~

A robust patch management process should be implemented to address security vulnerabilities, ensure compliance,
maintain uptime, and enable feature enhancements.

Securing the Kubernetes Orchestrator
------------------------------------

Kubernetes control plane API communication must be secured using TLS encryption, API authentication (e.g., via LDAP),
etc. Unsecured control plane nodes represent a significant threat; harden them by disabling unused ports and
prohibiting root access.

Security recommendations for the orchestration manager include:

- Cluster management network isolation to protect the control plane and restrict administrative command execution.
  Use network isolation techniques, configure RBAC on the cluster manager, and configure node service accounts using
  the principle of least privilege.
- Enforce access control on registries using unique credentials to limit who can control builds or add images.
- Use TLS for all network access.
- Configure user roles and access levels to ensure segregation of duties.

   - Do not co-locate container and non-container services on the same node.
   - Do not run containers as root.

- Implement multi-factor authentication for all administrative access.
- Harden the configuration using Center for Internet Security (CIS) benchmarks for container runtimes and Kubernetes.
- Deploy security products providing allowlisting, behavior monitoring, and anomaly detection to prevent malicious
  activity.
- Avoid privileged container applications through policy management to mitigate potential attacks.
- Integrate with other security ecosystems (SIEM).
- Isolate environments (dev/test/production) within the cluster.
- Create administrative boundaries between resources using namespaces and avoid using default namespaces.
- Enable Seccomp to restrict actions available within container applications.
- Limit discovery by restricting access to cluster management metadata on configurations, containers, and nodes.

Control Network Access to Sensitive Ports
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kubernetes clusters use a range of ports, making them potential attack targets. Configure authentication and
authorization on the cluster and nodes. The Kubernetes documentation :cite:p:`k8s-documentation-ports-and-protocols`
details default ports. Block access to unnecessary ports and limit access to the Kubernetes API server to trusted
networks only.

**Control Plane Node(s):**

======== ========== ======================
Protocol Port Range Purpose
======== ========== ======================
TCP      6443       Kubernetes API Server
TCP      2379-2380  etcd server client API
TCP      10250      Kubelet API
TCP      10259      kube-scheduler
TCP      10257      kube-controller-manager
======== ========== ======================

**Worker Nodes:**

======== =========== =================
Protocol Port Range  Purpose
======== =========== =================
TCP      10250       Kubelet API
TCP      30000-32767 NodePort Services
======== =========== =================

Controlling Access to the Kubernetes API
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Kubernetes API is a primary security target. Control access and allowed actions carefully.

Using Transport Layer Security and Service Mesh
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Secure inter-service communication within the cluster using TLS, encrypting all traffic by default. Kubernetes expects
default TLS encryption for API communication; most installation methods facilitate certificate creation and
distribution.

.. note::

  Some components and installation methods might enable local ports over HTTP. Administrators should review component settings to
  identify potential unsecured traffic.

Service meshes (e.g., Linkerd, Istio) provide default TLS encryption and additional telemetry. A service mesh uses
layer 7 proxies for service-to-service communication, comprising data plane (proxies paired with microservices) and
control plane (proxy configuration, TLS certificate and policy management) components.
NIST SP 800-204A :cite:t:`nist-800-204a` and NIST SP 800-204B :cite:t:`nist-800-204b` provide guidance on deploying
service meshes.

API Authentication and Authorization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Secure Kubernetes cluster connections using the following authentication mechanisms:

- Configure user roles and access levels for segregation of duties (RBAC).
- Use multi-factor authentication for all administrative access.
- Use token-based or certificate-based service and session authentication.
- Integrate with existing identity management platforms (e.g., SAML, AD) for access control.

Restricting Access to etcd and Encrypting Contents Within etcd
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

etcd, a critical Kubernetes component storing state and secrets, requires robust protection. Write access to the API
server's etcd grants root access to the entire cluster; even read access can be exploited for privilege escalation.

The Kubernetes scheduler uses etcd to find unscheduled pods, sending them to available kubelets. The API server
validates submitted pods before writing them to etcd. Directly writing to etcd bypasses many security mechanisms
(e.g., PodSecurityPolicies).

Use strong credentials (e.g., mutual TLS authentication via client certificates) for API server-etcd communication.
Isolate etcd servers behind a firewall accessible only by the API servers.

Controlling Access to the Kubelet
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kubelets expose HTTPS endpoints controlling nodes and containers. Production clusters should enable kubelet
authentication and authorization (unauthenticated access is insecure by default).

Securing the Kubernetes Dashboard
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Kubernetes dashboard, a web application for cluster management (not a core Kubernetes component), requires careful
security configuration. Many tutorials create highly privileged service accounts, making it a vulnerability (Reference:
Tesla cloud resources are hacked to run cryptocurrency-mining malware :cite:p:`arstechnica-tesla`).

To prevent dashboard attacks:

- Do not publicly expose the dashboard without additional authentication.
- Enable RBAC to limit the dashboard's service account privileges.
- Review and restrict the service account's assigned privileges.
- Implement granular permissions per user.
- Block dashboard requests from internal pods using network policies (kubectl proxy will still function).
- Verify that no cluster admin role binding exists (a vulnerability in versions prior to 1.8).
- Deploy the dashboard with an authenticating reverse proxy and multi-factor authentication (using embedded OpenID
  Connect (OIDC) id_tokens or Kubernetes Impersonation). This allows using user credentials instead of a privileged
  ServiceAccount, suitable for on-prem and managed cloud clusters.

Using Namespaces to Establish Security Boundaries
-------------------------------------------------

Kubernetes namespaces provide the first level of isolation between components. Apply security controls (network
policies, pod policies, etc.) to workloads in separate namespaces.

Separating Sensitive Workloads
------------------------------

Run sensitive workloads on dedicated nodes to minimize the impact of a compromise. This reduces the risk of accessing
sensitive applications through less secure applications sharing a runtime or host. Node pools and Kubernetes namespaces
can facilitate this separation.

Creating and Defining Network Policies
--------------------------------------

Network policies control network access to cloud-native applications. Define clear ingress and egress policies and
modify default policies (e.g., blocking or allowing traffic from other namespaces/clusters) where policy support is
enabled.

Running the Latest Version
--------------------------

Regularly update to the latest Kubernetes release to benefit from new security features and patches.

Securing Platform Metadata
--------------------------

Kubernetes metadata contains sensitive information (including kubelet admin credentials). Secure it using encryption to
prevent theft and privilege escalation.

- Limit access to cluster management metadata (configurations, containers, nodes).
- Ensure all metadata is encrypted and network access runs over TLS.

Enabling Logging and Monitoring
-------------------------------

Enable and monitor audit logs for anomalous or unauthorized API calls, paying close attention to authorization
failures. Logging, monitoring, and alerting are critical for Kubernetes security.

Runtime Security
----------------

Container runtime best practices include:

- Integrate runtime processes with Security Information and Event Monitoring (SIEM).
- Use container-aware runtime defense tools.
- Ensure all applications are from secure and verified images.
- Do not run applications with root privileges.
- Properly segment sensitive workloads using namespaces or clusters to limit the impact of compromises.

User Namespaces for Enhanced Isolation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A primary security concern in containerized environments is a container breakout, where an attacker escapes the
container's boundaries to gain control over the underlying host. A key enabler for this is when a container runs as the
root user, as this user ID (UID 0) is the same as the root user on the host.

The User Namespaces feature in Kubernetes directly mitigates this risk. It allows a Pod to run in a separate user
namespace where the internal user (e.g., root) is mapped to a high-numbered, non-privileged user on the host. This
isolation ensures that even if an attacker compromises a container running as root, they do not have root privileges on
the host node, significantly limiting their ability to cause damage.

Starting with Kubernetes 1.33, the platform will have the User Namespaces feature enabled to enhance
workload isolation and enforce the principle of least privilege at the host level.

Secrets Management
------------------

Apply the principle of least privilege to secrets management in Kubernetes:

- Applications should only access necessary secrets.
- Use different secrets for different environments (production, development, testing).

Protect secret values (sensitive data) at rest and in transit. TLS encrypts traffic between Kubernetes control plane
and worker nodes.

Avoid storing secrets in scripts or code; instead, provide them dynamically at runtime. Use a secure data repository
(key manager, vault) for sensitive data (SSH keys, API keys, database credentials). Retrieve credentials on demand over
secure channels to prevent writing unprotected data to disk. Back up key manager or vault encryption keys using a FIPS
140-2 Hardware Security Module.

- Check for hardcoded passwords, keys, and other sensitive items in container applications.
- Use security tools to automate scanning for hardcoded sensitive items.

Trusted Registry
----------------

Use trusted container registries accepting images only from validated sources. For third-party images, establish a
formal validation process ensuring compliance with security requirements. Enforce access control using unique
credentials to limit who can control builds or add images.

- Secure registry network access using TLS/SSL/VPN.
- Validate and scan container applications for viruses and vulnerabilities. Deploy only images signed with trusted keys.
- Use image versioning to ensure the latest certified applications are deployed.
- Trusted registries should reject improperly signed containers.
- Use approved registries for production images.
- Consider using third-party products for pre- and post-deployment container validation.

Remove stale, unsafe, and vulnerable images from the registry (using time triggers and image labels).

Isolation
---------

VM versus Container Isolation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Directly comparing container and VM isolation is misleading. They differ fundamentally:

- **VMs:** Provide hard isolation at the layers underlying application software.
- **Containers:** Rely on OS, container runtime, and Kubernetes software-based mechanisms. Container workloads are sets
  of Linux processes; additional software-based isolation (e.g., kernel namespaces) is possible.

The primary isolation mechanism in Kubernetes should be VM-based or physical machine-based. Deploy multiple
applications in the same Kubernetes cluster only after careful planning and verification of their compatibility. The
default recommendation is one namespace per Cloud-Native Network Function (CNF).

Container Isolation in the Kubernetes Cluster
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Namespaces
^^^^^^^^^^

Use Kubernetes namespaces for resource isolation within a cluster. Do *not* use them to isolate deployment stages
(development, production, testing). Dedicated clusters provide the most reliable separation for sensitive workloads.
