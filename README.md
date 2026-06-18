## Multi-Node Deployment of Resume Matcher on Kubernetes using Kind

Implemented a multi-node Kubernetes cluster using Kind on Windows, deployed the Resume Matcher application from GHCR, and demonstrated advanced Kubernetes scheduling with Node Affinity, Taints, and Tolerations.

## Access the walkthrough

[![Kind Cluster Walkthrough](https://img.youtube.com/vi/NX680uLoMpg/0.jpg)](https://www.youtube.com/watch?v=NX680uLoMpg)

[Watch the YouTube Video](https://www.youtube.com/watch?v=NX680uLoMpg)

---

This tutorial provides a comprehensive walkthrough. Watch the video above to learn more.

# 🛠 Deployment Strategy

# Step 1: Kind Installation & Verification

Downloaded and installed kind.exe
Added Kind binary to Windows PATH
Verified installation with:
kind version
<div align="center">
<img src="images/kind/S1 KIND/kinds1.1.png" width="250"/>
<img src="images/kind/S1 KIND/kinds1.2.png" width="250"/>
<img src="images/kind/S1 KIND/kinds1.3.png" width="250"/>
<img src="images/kind/S1 KIND/kinds1.4.png" width="250"/>
</div>

# Step 2: Multi-Node Cluster Creation
Created a Kind cluster with:
1 Control Plane
3 Worker Nodes
Configured custom networking
Verified all nodes reached Ready state
Added zone labels:
kubectl label node kind-node-worker zone=east
kubectl label node kind-node-worker2 zone=west
kubectl label node kind-node-worker3 zone=central
<div align="center">
<img src="images/kind/S2 KIND/kinds2.1.png" width="250"/>
<img src="images/kind/S2 KIND/kinds2.2.png" width="250"/>
<img src="images/kind/S2 KIND/kinds2.3.png" width="250"/>
</div>


# Step 3: GitHub Actions CI/CD & GHCR
Configured GitHub Actions workflow
Built multi-architecture Docker images
Published images to GitHub Container Registry (GHCR)
Verified image availability using Docker pull
<div align="center">
<img src="images/kind/S3 KIND/kinds3.1.png" width="250"/>
<img src="images/kind/S3 KIND/kinds3.2.png" width="250"/>
<img src="images/kind/S3 KIND/kinds3.3.png" width="250"/>
<img src="images/kind/S3 KIND/kinds3.4.png" width="250"/>
<img src="images/kind/S3 KIND/kinds3.5.png" width="250"/>
<img src="images/kind/S3 KIND/kinds3.6.png" width="250"/>
<img src="images/kind/S3 KIND/kinds3.7.png" width="250"/>
<img src="images/kind/S3 KIND/kinds3.8.png" width="250"/>
<img src="images/kind/S3 KIND/kinds3.9.png" width="250"/>
</div>


# Step 4: Node Affinity Scheduling
Applied Node Affinity rules targeting zone=east
Deployed Resume Matcher application
Verified pods scheduled exclusively on east worker node
<div align="center">
<img src="images/kind/S4 KIND/kind10.png" width="250"/>
<img src="images/kind/S4 KIND/kind11.png" width="250"/>
<img src="images/kind/S4 KIND/kind12.png" width="250"/>
<img src="images/kind/S4 KIND/kind13.png" width="250"/>
</div>


# Step 5: Application Deployment with ConfigMaps & Secrets
Created ConfigMaps and Secrets
Configured GHCR imagePullSecret
Deployed PostgreSQL and Resume Matcher workloads
Exposed application using NodePort and Port Forwarding
<div align="center">
<img src="images/kind/S5 KIND/kinds5.1.png" width="250"/>
<img src="images/kind/S5 KIND/kinds5.2.png" width="250"/>
<img src="images/kind/S5 KIND/kinds5.3.png" width="250"/>
<img src="images/kind/S5 KIND/kinds5.4.png" width="250"/>
<img src="images/kind/S5 KIND/kinds5.5.png" width="250"/>
<img src="images/kind/S5 KIND/kinds5.6.png" width="250"/>
<img src="images/kind/S5 KIND/kinds5.7.png" width="250"/>
<img src="images/kind/S5 KIND/kinds5.8.png" width="250"/>
</div>


# Step 6: Node Affinity Migration
Updated affinity rules from zone=east to zone=west
Restarted deployment
Verified pods automatically migrated to west worker node
<div align="center">
<img src="images/kind/S6 KIND/kinds6.1.png" width="250"/>
<img src="images/kind/S6 KIND/kinds6.2.png" width="250"/>
<img src="images/kind/S6 KIND/kinds6.3.png" width="250"/>
</div>


# Step 7: Taints & Tolerations
Applied taint to west worker node:
kubectl taint nodes kind-node-worker2 dedicated=db:NoSchedule
Added tolerations to deployment
Verified workloads continued running on tainted node
<div align="center">
<img src="images/kind/S7 KIND/kinds7.1.png" width="250"/>
<img src="images/kind/S7 KIND/kinds7.2.png" width="250"/>
<img src="images/kind/S7 KIND/kinds7.3.png" width="250"/>
<img src="images/kind/S7 KIND/kinds7.4.png" width="250"/>
</div>


# Step 8: Scheduling Failure Without Tolerations
Removed tolerations from deployment
Restarted workloads
Observed pods remain in Pending state
Verified taints prevented scheduling
<div align="center">
<img src="images/kind/S8 KIND/kinds8.1.png" width="250"/>
<img src="images/kind/S8 KIND/kinds8.2.png" width="250"/>
</div>


# Step 9: Untainting Node
Removed node taint
Restarted deployment
Verified pods returned to Running state
<div align="center">
<img src="images/kind/S9 KIND/kinds9.png" width="250"/>
</div>

# 📝 Notes
Kind: Multi-node local Kubernetes cluster
GitHub Actions: Automated CI/CD pipeline
GHCR: Container registry for application images
Node Affinity: Controlled pod placement using labels
Taints & Tolerations: Demonstrated scheduling restrictions and exceptions
Secrets & ConfigMaps: Secure configuration management
Outcome: Successfully deployed a production-style Resume Matcher application on a 4-node Kind cluster while demonstrating advanced Kubernetes scheduling concepts.
