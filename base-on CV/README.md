# 🧩 I. TECHNICAL QUESTIONS (Based on CV)

## 📌 1. About the CI/CD Pipeline project

### Can you explain in detail how you implemented the CI/CD pipeline?

I used GitHub Actions to automate the CI/CD process. The pipeline was triggered on every push to the main branch, running unit tests, static code analysis using SonarQube, vulnerability scanning with Trivy, and finally deploying Dockerized microservices to AWS infrastructure provisioned by Terraform.

### Why did you choose GitHub Actions over Jenkins or GitLab CI?

GitHub Actions is integrated with GitHub, easy to configure, and has reusable workflows. For a small-scale project, it provided faster setup and lower maintenance compared to Jenkins.

### How did you integrate SonarQube and Trivy into the pipeline?

SonarQube was used via an official GitHub Action that scanned the codebase for quality and security issues. Trivy was run as a separate step after Docker build to scan for vulnerabilities in the container image.

### How do you manage secrets securely in GitHub Actions?

I store secrets in GitHub's encrypted Secrets storage and reference them using ${{ secrets.MY_SECRET }} syntax. This ensures credentials are not hardcoded or exposed in logs.

### What would you do if Trivy reported a "High" severity vulnerability?

I would first verify if the vulnerability is in a component I use directly. If so, I would upgrade or patch the component. If it’s a transitive dependency, I’d look for secure alternatives or use image hardening techniques.

## 📌 2. About Redpanda Architecture Analysis

### What is the key difference between Redpanda and Apache Kafka?

Redpanda is a Kafka-compatible streaming platform that is written in C++ and does not require JVM or ZooKeeper, making it lightweight and faster in certain scenarios.

### What kind of problems are Redpanda and Kafka used to solve?

Both Redpanda and Kafka are used to build real-time data streaming applications. They are ideal for handling use cases like event-driven architectures, log aggregation, stream processing, real-time analytics, and decoupled microservices communication.

### What performance metrics did you measure and how did you use Prometheus/Grafana?

I measured CPU usage, memory consumption, disk I/O, and throughput. Prometheus collected these metrics using exporters, and Grafana visualized them in dashboards for benchmarking Redpanda's performance.

### Did you face any difficulties during the benchmarking process?

Yes. At first, the performance data from Prometheus was inconsistent due to misconfigured scraping intervals. I fixed it by tuning the Prometheus configuration and validating exporters individually before combining the dashboard views.

## 📌 3. About AWS Skills

### What is Amazon Web Services (AWS) and what are its key features?

Amazon Web Services (AWS) is a cloud computing platform that offers a vast range of services, including computing power, storage, and databases, to help businesses scale and grow more cost-effectively.

#### Key Features of AWS

1. Scalability and Elasticity: AWS provides tools that allow for both vertical and horizontal scaling, as well as the ability to auto-scale based on demand.

2. Global Reach: With data centers in multiple geographic regions, AWS enables businesses to operate on a global scale while remaining compliant with local regulations.

3. Pay-As-You-Go Pricing: This flexible pricing model allows users to pay only for the resources they consume, reducing upfront costs.

4. Security and Compliance: AWS offers a variety of security tools and features to help protect data, as well as compliance with numerous industry standards.

5. Hybrid Capabilities: AWS supports hybrid architectures, allowing businesses to integrate their existing on-premises solutions with the cloud.

6. Artificial Intelligence and Machine Learning: With AWS, businesses can harness the power of AI and ML through accessible services for data processing, analysis, and more.

7. Developer Tools: From code repository management to continuous integration and deployment, AWS provides a comprehensive suite of developer-centric services.

8. Internet of Things (IoT): AWS offers capabilities for managing and processing IoT data, connecting devices securely to the cloud.

### Describe the difference between Elastic IP and Public IP in AWS.

In AWS, every EC2 instance automatically gets a Public IP and can optionally be assigned an Elastic IP for more flexibility.

#### Public IP

- Dynamic: Assigned when the instance starts and lost on stop or termination.
- Shared: Drawn from a pool of AWS addresses, potentially used by other instances.
- Cost: Free while associated with a running instance.
- Useful for instances that need temporary, internet-facing access.

#### Elastic IP

- Static: Remains constant until explicitly released.
- Dedicated: Solely assigned to the AWS account unless released.
- Cost: Incurs charges when not in use with a running instance.
-Designed for hosting applications or network appliances that require a consistent public IP address.

#### Best Practices

Public IP: Let instances use public IPs unless there's a specific need for a static address. Avoid leaving unused Elastic IPs assigned to instances, as this costs money. Instead, consider releasing them and using other appropriate mechanisms, such as public IPs or AWS resources like load balancers and NAT gateways.

### Which AWS services have you used in your projects?

I’ve used EC2 for computing, S3 for storage, IAM for access control, and CloudWatch for monitoring. I also provisioned infrastructure using Terraform.

### What is AWS Identity and Access Management (IAM) and why is it important?
AWS Identity and Access Management (IAM) is a free AWS service that grants secure access to AWS resources. It enables you to control who can use your AWS resources (authentication) and how they can use them (authorization).

#### Key Components
1. Users: These are the end users who would be accessing the AWS resources. They can be grouped together according to the designations or roles.

2. Groups: Groups are a way to combine several users so that they can be assigned the same set of permissions. This makes managing permissions easier, especially in scenarios where multiple users require similar levels of access.

3. Roles: IAM roles are created and then assigned to other AWS resources or AWS accounts. They eliminate the need to share long-term credentials. Instead, they allow for secure access to resources.

### Why IAM is important
1. IAM is fundamental to AWS security and offers several advantages:

2. Principle of Least Privilege: Ensures users and resources have only the permissions they need to perform their tasks, reducing risks.

3. Granular Permissions: AWS provides a vast range of services, and within each service, there are numerous actions. IAM allows for specific actions on particular services to be granted, offering a great degree of control.

4. Access Management to Resources: IAM not only manages access for users and groups but also for services, ensuring secure communication between AWS resources.

5. Secure Access Sharing: Using roles, AWS allows for secure cross-account sharing. This is used by organizations that have multiple AWS accounts to enforce security and centralize management.

6. Compliance Tracking: IAM provides detailed logs to track user activity, which is crucial for compliance with industry standards.

7. Password Policies: IAM allows for strong password policies, ensuring user authentication methods comply with security best practices.

### Describe the different EC2 instance types and their use cases.

Amazon EC2 offers a broad range of instance types optimized to fit different use cases. These types can be categorized into groups like General Purpose, Compute Optimized, Memory Optimized, Storage Optimized, and Accelerated Computing.

#### General Purpose
##### Use Cases

These instance types are suitable for a diverse array of workloads, from small to medium databases to development and testing environments.

##### Burstable Performance

- T2: Designed for cost-efficient applications with short bursts of CPU usage. Accumulates CPU credits during low usage, which can then be used during traffic spikes.

#### Compute Optimized
##### Use Cases
Ideal for compute-bound applications requiring high performance from the CPU.

- C5: Utilizes high-frequency Intel Xeon Scalable processors.
- C6g and C6gn: Powered by AWS Graviton2 processors, which are based on Arm architecture, and provide the best price-performance in the compute-optimized category.

#### Memory Optimized
##### Use Cases
Suited for memory-intensive applications like high-performance databases, distributed memory caches, and in-memory analytics.

- X1e: Offers the most memory in a single instance.
- R6g and R6gn: Utilizes AWS Graviton2 processors and provides a balance of compute, memory, and networking resources at a lower cost.

#### Storage Optimized

##### Use Cases
Designed for applications demanding high, sequential read and write access to very large data sets, like data warehousing and Hadoop clusters.

- I3: Utilizes Non-Volatile Memory Express (NVMe)-based SSDs for extremely high random I/O performance.
- D2: Cost-effective option for workloads that require high sequential read/write performance.

#### Accelerated Computing
##### Use Cases
Ideal for compute-intensive workloads that can benefit from the parallel processing capabilities of GPUs.

- P3: Equipped with NVIDIA Tesla V100 GPUs, suitable for deep learning, computational fluid dynamics, and computational finance.
- G4dn: Combines NVIDIA T4 GPUs with custom Intel Cascade Lake CPUs, optimized for gaming, machine learning, and 3D visualization.
- F1 and A1: Designed for specific workloads using FPGAs (Field-Programmable Gate Arrays) and AWS Inferentia, respectively

### How would you deploy a microservices app on AWS?

I’d use Terraform to provision infrastructure, Docker to containerize each service, and host them on EC2 or ECS. A load balancer would distribute traffic, and IAM would control access.

### What do you know about IAM and how do you apply least privilege?

IAM allows managing access to AWS resources. I create roles with minimal required permissions and assign them to services/users, following the principle of least privilege.

### What was the most challenging part of working with AWS?

One challenge was debugging failed deployments due to misconfigured IAM roles. I learned to use IAM policy simulator and CloudTrail logs to trace denied actions and adjust permissions incrementally. Another challenge was managing cost while testing, so I used budget alarms and resource tagging.

## 📌 4. About Docker and Docker Compose

### Can you describe your docker-compose.yml structure?

It defined multiple services (e.g., web, db), shared a custom network, used environment variables, and volume mounts. Dependencies were managed via depends_on.

### How did you solve container communication issues in Docker Compose?

I ensured services were on the same network and used service names as hostnames. I also checked port mappings and container logs to troubleshoot issues.

### What difficulties did you encounter while working with Docker?

One difficulty was conflicting ports when running multiple services locally. I solved this by configuring dynamic ports and isolating network bridges. I also encountered volume permission issues, which were resolved by adjusting user permissions inside the Dockerfile.

## 📌 5. About Security & CTF Practice

### Which lab on HackTheBox or TryHackMe was most memorable? What did you learn?

One lab on TryHackMe simulated a privilege escalation attack. I learned how misconfigured SUID binaries can be exploited and how to patch such vulnerabilities.

### What are common web application vulnerabilities you know?

SQL Injection, Cross-Site Scripting (XSS), Cross-Site Request Forgery (CSRF), and Insecure Deserialization are among the top OWASP vulnerabilities.

### Have you ever failed a CTF challenge? What did you do next?

Yes. Some challenges involving binary exploitation were too advanced for my level initially. I bookmarked them, reviewed community write-ups, and later revisited the boxes after studying relevant techniques like buffer overflow and format string attacks.

## 📌 6. About Kubernetes Networking

### How do pods communicate with each other in Kubernetes?

In Kubernetes, each pod is assigned a unique IP address within the cluster. Pods communicate with each other using this IP over a flat network model provided by the CNI (Container Network Interface) plugin. DNS is also used to resolve service names to pod IPs, enabling inter-pod communication without hardcoding IPs.

### How do containers communicate with each other inside the same pod?

Containers within the same pod share the same network namespace. This means they share the same localhost IP (127.0.0.1) and ports. They can communicate over localhost just like processes on the same machine, making communication between them efficient and fast.

## 7. Android Project

### Can you describe the architecture of your pothole detection system?

Sure. The system consists of an Android application that detects potholes using phone sensors and sends the data to a backend server built with Spring Boot. The server receives location and pothole information and stores it in a PostgreSQL database.  

I used REST APIs for communication between the mobile app and the backend. For development and testing, the backend ran in a Docker container. In the future, I plan to integrate it with AWS services for better scalability.


### What technologies did you use for the backend, and why?

I chose Spring Boot for the backend because it's powerful, has good support for REST APIs, and integrates well with PostgreSQL. Spring Data JPA also made it easier to handle database operations.  

PostgreSQL was selected because it's reliable and performs well for geolocation-based queries, which was essential for storing and querying pothole locations.


### Did you containerize the backend or use any CI/CD tools?

Yes. I containerized the backend using Docker to ensure consistency across environments. I also wrote a basic GitHub Actions workflow to automatically build and test the backend whenever changes were pushed.  

This helped me understand how CI/CD pipelines work and how they can improve the software development workflow.


### How did your Android app communicate with the backend API?

The Android app sent data to the backend using HTTP requests with JSON payloads. I implemented a RESTful API in Spring Boot that received the pothole data and stored it in the database.  

I also made sure to handle edge cases like failed requests or timeouts by implementing retry mechanisms on the mobile side.


### How did you design your database schema to store pothole data?

I created a table with fields like `id`, `latitude`, `longitude`, `timestamp`, and `severity`. The coordinates are indexed to allow fast lookup based on location, which is important for future features like alerting users when they’re near a reported pothole.


### Did you consider any security practices in your backend system?

Since this was a personal project, I didn’t fully implement authentication, but I planned to use JWT for secure access and HTTPS for secure communication. I also avoided exposing sensitive endpoints and handled invalid data properly to prevent injection attacks.


### If you wanted to scale this system to support an entire city, what would you improve?

I would deploy the backend on cloud infrastructure like AWS or GCP. I’d use a managed database like Amazon RDS, add caching with Redis for frequently accessed data, and use a queue system like Kafka for better handling of incoming data streams.  

I would also implement load balancing, auto-scaling, and centralized logging and monitoring with tools like ELK or Prometheus-Grafana.

# 🧽 II. BEHAVIORAL QUESTIONS (Based on experience and motivation)

### 💡 Why did you shift your focus to DevOps/Security?

I started with backend development but realized system reliability and security are just as crucial. I became passionate about infrastructure, automation, and protection, which led me to learn CI/CD, Cloud, and security practices through CTFs.

### 🤝 How did you collaborate with others in a team project?

In the Realtime Pothole Detector project, I handled the backend and API logic, frequently syncing with the frontend team to ensure data formats matched and features were integrated smoothly.

### 🌟 How do you learn new technologies outside of your coursework?

I use official documentation, online courses (e.g., AWS Academy, Cisco), and hands-on platforms like GitHub, TryHackMe, and HackTheBox. I often clone open-source projects to learn by improving them.

### 😅 Describe a situation where you encountered failure or difficulty during a project.

During my first deployment of a CI/CD pipeline, the Docker container continuously crashed due to an incorrect health check endpoint. It took hours of debugging logs and networking issues before I realized the app wasn’t listening on the expected port. From that experience, I learned to validate assumptions early and use logging effectively.

## 🔄 III. RAPID-FIRE QUESTIONS

### What is an SSH key and why is it used?

An SSH key is a secure credential used for authenticating with remote systems, enabling passwordless login and encrypted communication.

### How do you perform rollback in a CI/CD pipeline?

I either re-deploy a previous stable version from the image repository or automate rollback via pipeline stages triggered on deployment failure.

### What do you do if the pipeline fails due to test errors?

I check logs to identify failing tests, fix the code or test cases, and rerun the pipeline after verifying locally.

### Why use containers instead of direct installation on the host?

Containers isolate environments, ensure consistency, reduce conflicts, and allow rapid scaling and deployment.

### Which do you secure first: frontend or backend?

I prioritize backend security first as it handles data, logic, and access control, but both layers need attention for full-stack protection.

