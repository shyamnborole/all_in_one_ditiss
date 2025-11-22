# ITIM and DevOps - Answers (1-10)

1. **What is ITIL? What is V3?**
   - **ITIL (Information Technology Infrastructure Library):** A set of detailed practices for IT service management (ITSM) that focuses on aligning IT services with the needs of business.
   - **ITIL V3 (2007 Edition):** Also known as ITIL 2007, it introduced the ITIL service lifecycle, which includes five stages:
     - Service Strategy
     - Service Design
     - Service Transition
     - Service Operation
     - Continual Service Improvement (CSI)
   - ITIL V3 was superseded by ITIL 4 in 2019, which provides a more flexible and holistic approach to ITSM.

2. **Explain Software Development Life Cycle.**
   - **SDLC** is a process used by the software industry to design, develop, and test high-quality software.
   - **Phases of SDLC:**
     - Requirement Gathering and Analysis
     - System Design
     - Implementation (Coding)
     - Testing
     - Deployment
     - Maintenance
   - **Models:** Waterfall, Agile, Iterative, Spiral, V-Model, etc.

3. **Explore Agile Development. What is scrum?**
   - **Agile Development:** An iterative and incremental approach to software development that emphasizes flexibility, customer collaboration, and rapid delivery.
   - **Key Principles:** 
     - Individuals and interactions over processes and tools
     - Working software over comprehensive documentation
     - Customer collaboration over contract negotiation
     - Responding to change over following a plan
   - **Scrum:** A framework within Agile for managing complex projects.
     - **Roles:** Product Owner, Scrum Master, Development Team
     - **Artifacts:** Product Backlog, Sprint Backlog, Increment
     - **Events:** Sprint, Sprint Planning, Daily Stand-up, Sprint Review, Sprint Retrospective

4. **What is Data Center?**
   - A data center is a facility that houses computing resources and related equipment for the purpose of collecting, storing, processing, and distributing large amounts of data.
   - **Key Components:**
     - Servers, storage systems, networking equipment (switches, routers)
     - Power supply (redundant, backup generators)
     - Cooling systems
     - Physical security (access controls, surveillance)
   - **Types:** Enterprise, Colocation, Cloud, Edge

5. **What is the functionality of a hypervisor?**
   - A hypervisor (or virtual machine monitor) is software that creates and runs virtual machines (VMs).
   - **Functions:**
     - Abstraction of physical hardware resources (CPU, memory, storage, networking)
     - Allocation of these resources to multiple VMs
     - Isolation between VMs for security and stability
   - **Types:**
     - Type 1 (Bare-metal): Runs directly on hardware (e.g., VMware ESXi, Microsoft Hyper-V, Xen)
     - Type 2 (Hosted): Runs on top of an operating system (e.g., VMware Workstation, Oracle VirtualBox)

6. **What is Virtualization? What is difference between Type I, Type II virtualization, and containerization?**
   - **Virtualization:** The process of creating a virtual (rather than physical) version of something, such as an operating system, server, storage, or network.
   - **Type I (Bare-metal):** Hypervisor installed directly on the physical server. More efficient and secure. Used in enterprise environments.
   - **Type II (Hosted):** Hypervisor runs on top of a host OS. Less efficient but easier to set up. Used for development and testing.
   - **Containerization:** A lightweight form of virtualization that runs applications in isolated user spaces (containers) on a single OS kernel. 
     - **Differences:**
       - Virtualization virtualizes the entire machine, including the OS, while containerization virtualizes the OS to run multiple isolated user spaces.
       - Containers are more lightweight, start faster, and have less overhead than VMs.

7. **What is cloud computing? Explain cloud service models: IaaS, PaaS, SaaS, FaaS, DaaS.**
   - **Cloud Computing:** Delivery of computing services (servers, storage, databases, networking, software, analytics) over the internet (the cloud).
   - **Service Models:**
     - **IaaS (Infrastructure as a Service):** Provides virtualized computing resources over the internet (e.g., AWS EC2, Azure VMs).
     - **PaaS (Platform as a Service):** Provides a platform allowing customers to develop, run, and manage applications without the complexity of infrastructure (e.g., Google App Engine, Heroku).
     - **SaaS (Software as a Service):** Software distributed over the internet on a subscription basis (e.g., Gmail, Salesforce).
     - **FaaS (Function as a Service):** A type of serverless computing where the cloud provider runs code in response to events (e.g., AWS Lambda, Azure Functions).
     - **DaaS (Desktop as a Service):** Virtual desktops delivered over the cloud (e.g., Amazon WorkSpaces, VMware Horizon).

8. **What are the differences between vertical and horizontal scaling? Which one would you prefer and why?**
   - **Vertical Scaling (Scaling Up):** Adding more resources (CPU, RAM) to an existing server.
     - **Advantages:** Simpler, no application changes required.
     - **Disadvantages:** Limited by hardware, downtime required, single point of failure.
   - **Horizontal Scaling (Scaling Out):** Adding more servers to the pool and distributing the load.
     - **Advantages:** Can scale indefinitely, fault-tolerant, no downtime.
     - **Disadvantages:** More complex, may require application changes (stateless design).
   - **Preference:** Horizontal scaling is generally preferred for modern applications because it offers high availability and can scale to handle increasing loads. However, the choice depends on the application and requirements.

9. **How to create EC2 instance in AWS?**
   - **Steps:**
     1. Log in to AWS Management Console and navigate to EC2.
     2. Click "Launch Instance".
     3. Choose an Amazon Machine Image (AMI) (e.g., Amazon Linux, Windows).
     4. Select an instance type (e.g., t2.micro) and click "Next".
     5. Configure instance details (number of instances, network, IAM role, etc.).
     6. Add storage (default is 8GB, but can be increased).
     7. Add tags (optional but recommended for identification).
     8. Configure security group (firewall rules to allow traffic, e.g., SSH, HTTP).
     9. Review and launch. Select an existing key pair or create a new one to connect to the instance.

10. **What is use of these AWS services - EC2, S3, SNS, EKS?**
    - **EC2 (Elastic Compute Cloud):** Provides scalable virtual servers (instances) in the cloud. Used for hosting applications, websites, and processing workloads.
    - **S3 (Simple Storage Service):** Object storage service for storing and retrieving any amount of data. Used for backup, static website hosting, and big data storage.
    - **SNS (Simple Notification Service):** Pub/sub messaging service for sending notifications to multiple subscribers (email, SMS, HTTP endpoints). Used for alerting and event-driven architectures.
    - **EKS (Elastic Kubernetes Service):** Managed Kubernetes service to run containerized applications. Used for deploying, managing, and scaling containerized applications using Kubernetes.
# ITIM and DevOps - Answers (11-28)

11. **What is DevOps? Explain DevOps life cycle.**
    - **DevOps:** A cultural and professional movement that stresses communication, collaboration, integration, automation, and measurement of cooperation between software developers and IT operations.
    - **DevOps Life Cycle:**
      - Plan: Requirement gathering and project planning
      - Code: Software development and version control
      - Build: Continuous integration and build automation
      - Test: Automated testing and quality assurance
      - Release: Release management and deployment
      - Deploy: Infrastructure provisioning and application deployment
      - Operate: Infrastructure management and monitoring
      - Monitor: Performance monitoring and feedback loop

12. **What is GIT? Explain GIT workflow.**
    - **GIT:** A distributed version control system that tracks changes in source code during software development.
    - **GIT Workflow:**
      - Initialize repository: `git init`
      - Add files to staging: `git add <file>`
      - Commit changes: `git commit -m "message"`
      - Push to remote: `git push origin <branch>`
      - Pull updates: `git pull origin <branch>`
      - Branch management: Create, merge, and delete branches
      - Conflict resolution: Handle merge conflicts

13. **What is GIT branching? How to implement it? Write commands to create branch, merge branch, and delete branch.**
    - **GIT Branching:** A feature that allows developers to diverge from the main line of development and work independently.
    - **Implementation:**
      - Create branch: `git branch feature-branch`
      - Switch to branch: `git checkout feature-branch` or `git switch feature-branch`
      - Create and switch: `git checkout -b feature-branch`
      - Merge branch: `git merge feature-branch` (while on target branch)
      - Delete branch: `git branch -d feature-branch` (local), `git push origin --delete feature-branch` (remote)

14. **What is Docker? Explain Docker architecture.**
    - **Docker:** A platform for developing, shipping, and running applications in containers.
    - **Docker Architecture:**
      - Docker Client: CLI for user commands
      - Docker Daemon: Background service managing containers
      - Docker Images: Read-only templates for creating containers
      - Docker Containers: Runnable instances of images
      - Docker Registry: Storage for Docker images (Docker Hub)
      - Docker Objects: Networks, volumes, plugins

15. **What is Docker image and container? Explain life cycle of Docker container.**
    - **Docker Image:** A read-only template with instructions for creating a Docker container.
    - **Docker Container:** A runnable instance of a Docker image.
    - **Container Life Cycle:**
      - Create: `docker create`
      - Start: `docker start`
      - Run: `docker run` (create + start)
      - Stop: `docker stop`
      - Pause: `docker pause`
      - Restart: `docker restart`
      - Remove: `docker rm`

16. **An application has two components i.e. MySQL database and Python Web application. Explain steps to containerize this application. How to use Docker compose?**
    - **Steps to Containerize:**
      1. Create Dockerfile for Python application
      2. Use official MySQL Docker image
      3. Create docker-compose.yml file
      4. Define services for web app and database
      5. Configure networking and volumes
      6. Build and run with `docker-compose up`
    - **Docker Compose Example:**
      ```yaml
      version: '3'
      services:
        web:
          build: .
          ports:
            - "5000:5000"
          depends_on:
            - db
        db:
          image: mysql:5.7
          environment:
            MYSQL_ROOT_PASSWORD: example
          volumes:
            - db_data:/var/lib/mysql
      volumes:
        db_data:
      ```

17. **What is orchestration? Which tools can be used for the same.**
    - **Orchestration:** Automated configuration, coordination, and management of computer systems and software.
    - **Tools:**
      - Kubernetes (most popular)
      - Docker Swarm
      - Apache Mesos
      - Amazon ECS
      - Red Hat OpenShift
      - Nomad

18. **What is Kubernetes? Explain Kubernetes architecture.**
    - **Kubernetes:** An open-source container orchestration platform for automating deployment, scaling, and management of containerized applications.
    - **Architecture:**
      - Control Plane (Master Nodes):
        - API Server: Entry point for all REST commands
        - etcd: Key-value store for cluster data
        - Scheduler: Assigns pods to nodes
        - Controller Manager: Regulates cluster state
      - Worker Nodes:
        - Kubelet: Agent running on each node
        - Kube-proxy: Network proxy and load balancer
        - Container Runtime: Docker, containerd, etc.
        - Pods: Smallest deployable units

19. **What is pod? How do you scale pods?**
    - **Pod:** The smallest and simplest Kubernetes object that represents a single instance of a running process in a cluster.
    - **Scaling Pods:**
      - Manual Scaling: `kubectl scale deployment/my-app --replicas=5`
      - Horizontal Pod Autoscaler (HPA): Automatically scales based on CPU/memory usage
      - Vertical Pod Autoscaler (VPA): Adjusts resource requests/limits
      - Cluster Autoscaler: Adds/removes nodes based on resource needs

20. **What is CI? What is CD? Which are popular tools for CI/CD pipeline?**
    - **CI (Continuous Integration):** Practice of merging all developers' working copies to a shared mainline several times a day.
    - **CD (Continuous Delivery/Deployment):** Automated delivery of applications to selected infrastructure environments.
    - **Popular CI/CD Tools:**
      - Jenkins (most popular open-source)
      - GitLab CI/CD
      - GitHub Actions
      - CircleCI
      - Travis CI
      - Azure DevOps
      - AWS CodePipeline

21. **What is Jenkins? Explain Jenkins architecture.**
    - **Jenkins:** An open-source automation server for CI/CD pipelines.
    - **Architecture:**
      - Master Node: Central coordination, manages builds
      - Agent Nodes: Execute build jobs (can be multiple)
      - Web Interface: User dashboard and configuration
      - Plugins: Extend functionality (Git, Docker, Kubernetes)
      - Jobs/Pipelines: Automated workflows defined as code
      - Workspace: Directory where builds are executed

22. **How would you create pipeline in Jenkins?**
    - **Steps to Create Pipeline:**
      1. Install Pipeline plugin
      2. Create new Pipeline job
      3. Define pipeline using Jenkinsfile (declarative or scripted)
      4. Jenkinsfile contains stages: Checkout, Build, Test, Deploy
      5. Example Declarative Pipeline:
        ```groovy
        pipeline {
            agent any
            stages {
                stage('Build') {
                    steps {
                        sh 'mvn compile'
                    }
                }
                stage('Test') {
                    steps {
                        sh 'mvn test'
                    }
                }
                stage('Deploy') {
                    steps {
                        sh 'mvn deploy'
                    }
                }
            }
        }
        ```

23. **What's the difference between continuous integration, continuous delivery, and continuous deployment?**
    - **Continuous Integration:** Developers merge code changes frequently, automated builds and tests run.
    - **Continuous Delivery:** Code changes are automatically built, tested, and prepared for release to production.
    - **Continuous Deployment:** Code changes that pass automated testing are automatically deployed to production.
    - **Key Difference:** Continuous Delivery requires manual approval for deployment, while Continuous Deployment is fully automated.

24. **What is Puppet? How it works?**
    - **Puppet:** A configuration management tool for automating infrastructure management.
    - **How it Works:**
      - Puppet Master: Central server storing configuration manifests
      - Puppet Agent: Runs on managed nodes, applies configurations
      - Manifest Files: Define desired state using Puppet DSL
      - Catalog: Compiled configuration for each node
      - Idempotent: Ensures same result regardless of initial state

25. **What is Nagios? How it works?**
    - **Nagios:** An open-source monitoring system for IT infrastructure.
    - **How it Works:**
      - Nagios Core: Monitoring engine and scheduler
      - Plugins: Scripts that perform checks (CPU, memory, disk, services)
      - Notification: Alerts via email, SMS when thresholds breached
      - Web Interface: Dashboard for viewing status and reports
      - Passive Checks: External applications send results to Nagios

26. **Explain Service portfolio management.**
    - **Service Portfolio Management:** Strategic management of IT services throughout their lifecycle.
    - **Components:**
      - Service Pipeline: Planned and developing services
      - Service Catalog: Live and available services
      - Retired Services: Phased-out services
    - **Purpose:** Ensure IT services align with business objectives and deliver value.

27. **Explain Business relationship management.**
    - **Business Relationship Management (BRM):** Process for maintaining positive relationships with business customers.
    - **Key Activities:**
      - Understanding customer needs and expectations
      - Managing customer satisfaction
      - Communicating service value and performance
      - Identifying new service opportunities
      - Resolving service-related issues and conflicts

28. **What is Service Design & its purpose?**
    - **Service Design:** ITIL process for designing new IT services and changes to existing services.
    - **Purpose:**
      - Ensure services meet business requirements
      - Design for scalability, security, and availability
      - Consider cost-effectiveness and efficiency
      - Plan for support and maintenance
      - Align with overall business strategy and architecture
	