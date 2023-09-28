# Azure Container Apps: Zero 2 Hero

Greetings to my fellow Technology Advocates and Specialists.

In this Session, I will provide complete details on __Azure Container Apps__

I had the Privilege to talk on this topic in __ONE__ Azure Communities:-

| __NAME OF THE AZURE COMMUNITY__ | __TYPE OF SPEAKER SESSION__ |
| --------- | --------- |
| __Azure Back to School - 2023__ | __Virtual__ |


| __EVENT ANNOUNCEMENTS:-__ |
| --------- |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bccgs4jyvm1tlkcihmvl.png) |


| __WHATS NEW IN AZURE CONTAINER APPS:-__ |
| --------- |
| Please refer to the Provided Link - https://learn.microsoft.com/en-us/azure/container-apps/whats-new |


| __AZURE CONTAINER APPS ROADMAP:-__ |
| --------- |
| Please refer to the Provided Link: https://github.com/orgs/microsoft/projects/540/views/1  |


| __AZURE CONTAINER APPS OVERVIEW:-__ |
| --------- |

| __#__ | __OVERVIEW POINTERS__ |
| --------- | --------- |
| 1. | Fully managed environment on a Serverless platform. |
| 2. | Run containers while leaving behind the concerns of managing cloud infrastructure and complex container orchestrators. |
| 3. | Use Case #1: __Deploy API endpoints__. |
| 4. | Use Case #2: __Hosting Background Processing Jobs__. |
| 5. | Use Case #3: __Handling Event Driven Processing__. |
| 6. | Use Case #4: __Running Microservices__. |


| __AZURE CONTAINER APPS COMPONENTS:-__ |
| --------- |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/r0w9hoo6k4f3sgri4nwj.png) |

| __#__ | __COMPONENTS__ | __DESCRIPTION__ |
| --------- | --------- | --------- |
| 1. | Environment | Isolation boundary around a collection of container apps, Same virtual network for multiple container apps in the same environment, Multiple container apps in the same environment writes logs to same log Analytics workspace. |
| 2. | Revisions | Container apps versioning, first revision is provisioned automatically when container app is deployed, can retain up to 100 revisions, split traffic between active revisions (running multiple revisions concurrently), gradually moving towards Blue Green Deployments. |
| 3. | Replica | As container app revision scales out, new instances of revisions are created. These instances are known as replica. |
| 4. | Containers | Grouped together in Pods inside revision snapshots. Supports any Runtime or Programming Language. |
| 5. | Container Apps(apps): | First type of compute resource. Apps are services that run continuously. If containers in an app fails, it restarts automatically. |  
| 6. | Container Apps(jobs): | Second type of compute resource. Jobs are tasks that start, run for finite duration and then exit. Each task is a single unit of work. Tasks can be executed - manually, scheduled, or event driven. |


| __WHAT IS APPLICATION LIFECYCLE MANAGEMENT IN AZURE CONTAINER APPS:-__ |
| --------- |
| 1. It revolves around __revisions__. |
| 2. More revisions are created as containers changes. |
| 3. When a New Revision is created - Azure Container App when updated with a revision scope change. |
| 4. Single Revision Mode: Deactivate old Revisions (Manually or automatically) with the option to reactivate later. |
| 5. Multiple Revision Mode: Allow the revisions to be available. |
| 6. Zero Downtime Deployment. |


| __WHAT IS ZERO DOWNTIME DEPLOYMENT OF AZURE CONTAINER APPS:-__ |
| --------- |
| 1. Zero downtime deployment has 2 factors to consider - a) Single revision mode; b) Multiple revision mode. |
| 2. Single revision mode: a) No downtime while creating a new revision; b) existing revision is not deactivated until new revision is created; c) If ingress is enabled, the existing revision continues to receive 100% of the traffic until the new revision is ready. |
| 3. Multiple revision mode: a) Its in our control when revisions are activated or deactivated; b) which revisions receives ingress traffic; c) Depending upon if __traffic splitting rule__ is configured with latest Revision set to true, traffic does not switch to latest revision  until its ready. |
| 4. A new revision is considered ready when one of its replicas starts and becomes ready. A replica is ready when all of its containers start and pass their startup and readiness probes. |


| __WHAT ARE THE CONDITIONS WHEN CONTAINERS IN REVISION ARE SHUTDOWN:-__ |
| --------- |
| 1. When a container app scales in. |
| 2. While deactivating a revision, containers in the revision are shutdown. |
| 3. When a container app is deleted. |


| __AZURE CONTAINER APPS PLANS:-__ |
| --------- |

| __#__ | __PLAN TYPES__ | __DESCRIPTION__ | 
| --------- | --------- | --------- |
| 1. | Dedicated | Customized compute options where you're billed for instances allocated to each workload profile. |
| 2. | Consumption | Serverless architecture, can scale in and out on-demand, can scale to zero, pay only for running apps and chosen when the container app does not have specific hardware requirements. |


| __AZURE CONTAINER APPS SCALING CHARACTERISTICS:-__ |
| --------- |

| __#__ | __SCALE CRITERIA__ | __DESCRIPTION__ |  __IMAGE__ | 
| --------- | --------- | --------- | --------- | 
| 1. | HTTP Traffic | The number of concurrent HTTP requests are split between former and new Container Apps Revision | ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b5cr713rq86tjo7dst41.png) |
| 2. | Event Driven | Scaling is determined by number of messages in the queue. | ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ihyr3ukeduw3r2l4tcg3.png) |
| 3. | CPU or Memory | Scaling is determined by increase of CPU and memory consumption. | - |
| 4. | KEDA Scaler | Individual microservices can scale according to any KEDA Scale trigger. | ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dlrylqc358of65baadyu.png) |


| __AZURE CONTAINER APPS STORAGE MOUNTS:-__ |
| --------- |
| Different types of storage for Container Apps: a.) __Container File System__; b.) __Ephemeral Storage__; c.) __Azure Files__ |

| __CONTAINER FILE SYSTEM:-__ |
| --------- |
| 1. Temporary and is lost when container is shutdown or restarted. |
| 2. Files are visible only to the process running in the current container. |
| 3. No Capacity Guarantee, depends upon the disk space allocated to the container. |

| __EPHEMERAL STORAGE:-__ |
| --------- |
| 1. Files are available until the lifetime of the replica. |
| 2. If the container in the replica is restarted, files in the volume are still available. |
| 3. Any containers in the replica can mount to the same volume. |
| 4. Multiple Ephemeral Volumes can be mounted to a container in the replica. |
| 5. Total amount of vCPUs allocated to Replica governs the available storage. |

| __AZURE FILES:-__ |
| --------- |
| 1. Files are available in file share. | 
| 2. Multiple containers can mount to the same file share whether they belong to another Replica, another Revision, or another container App. | 
| 3. Multiple file share can be mounted to a container. | 
 


| __AZURE CONTAINER APPS HEALTH PROBES:-__ |
| --------- |
| 1. Probes are setup using TCP or HTTP(s). |
| 2. Probes supported by Azure Container Apps - a.) Startup [if application started successfully] b.) Liveness [if application is still running and responsive.] c.) Readiness [if a replica is ready to handle requests.] |
| 3. HTTP Probes: Validates the status of application dependencies before reporting a healthy status. |
| 4. TCP Probes: Validates the status of application dependencies before reporting a healthy status. |


| __AZURE CONTAINER APPS SECURITY CONSIDERATIONS:-__ |
| --------- |
| 1. Manage Secrets. |
| 2. Managed Identities. |


| __MANAGE SECRETS:-__ |
| --------- |
| 1. __STORE SECRET IN CONTAINER APPS:-__  |
| a. Azure Container Apps allows to securely store sensitive values. |
| b. Secrets are defined at application level. These are then available to all revisions in the container apps.  |
| c. New Revisions is not created when we add, remove or change secrets. |
| d. One Application Revision can reference one or more secrets. |
| e. Multiple Application Revision can reference same secrets. |
| f. When a secret is updated or deleted, change is not reflected automatically to the existing revisions. So one of the 2 approaches should be considered - i.) Deploy a New Revision; ii.) Restart an existing revision. |
| g. After declaring secrets at the application level, we can reference them in volume mounts when you create a new revision in your container app. | 
| h. When secrets are mounted in a volume, each secret is mounted as a file in the volume. | 
| i. The file name is the name of the secret. | 
| j. The file contents are the value of the secret. | 
| k. We can load all secrets in a volume mount, or we can load specific secrets. |
| 2. __REFERENCE SECRET FROM KEY VAULT:-__  |
| a. Container Apps automatically retrieves the secret value from Key Vault. |
| b. To reference a secret from Key Vault, you must first enable managed identity in your container app and grant the identity access to the Key Vault secrets. |

| __MANAGED IDENTITIES:-__ |
| --------- |
| Azure Container Apps supports both a.) System Assigned Managed Identity; and b.) User Assigned Managed Identity. |



| __LIMITATIONS IN AZURE CONTAINER APPS:-__ |
| --------- |
| 1. Azure Container Apps cannot run privileged containers. |
| 2. Linux based container images are required. |
| 3. We can only add one of each probe type per container. |
| 4. Executables probes aren't supported. | 
| 4. Port values must be integers; Named ports aren't supported. |
| 5. gRPC isn't supported. |



__Hope You Enjoyed the Session!!!__

__Stay Safe | Keep Learning | Spread Knowledge__
