---
title: "VM permissions/scope updates for Google Kubernetes Engine with zero downtime — DevOps"
seoTitle: "VM permissions/scope updates for Google Kubernetes Engine with zero do"
seoDescription: "VM permissions/scope updates for Google Kubernetes Engine with zero downtime — DevOps"
datePublished: Sat Apr 22 2023 14:41:53 GMT+0000 (Coordinated Universal Time)
cuid: clgs39tzw000309mmf9xjej7c
slug: vm-permissionsscope-updates-for-google-kubernetes-engine-with-zero-downtime-devops
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1682174504227/8cff0f3e-17c0-4efc-8231-80d41520b75f.jpeg
tags: kubernetes, devops, containers, google-cloud-platform

---

*Want to utilize Cloud SQL, Datastore, or any other services from your pods running in Kubernetes Engine, and you intend to use the automatic VM credentials. However, the VM does not have the required scopes or permissions, and you cannot modify it.*

What steps can you take to resolve this issue?

Google Compute Engine VM includes a pre-configured OAuth2 Service Account, which enables automatic authentication to different GCP services. By assigning various “permissions” to this service account, you can control the scopes it has for accessing the services.

To illustrate, you could grant the “compute.readonly” scope to a service account, allowing it to solely read data from compute engine. Alternatively, you could assign the “compute.writeonly” scope to a different service account, giving it read and write access. Service accounts can have any combination of scopes, allowing you to provide them with the precise permissions required for their intended tasks. [A comprehensive list of all Google scopes is available for reference.](https://developers.google.com/identity/protocols/oauth2/scopes)

*Here is a GCP article on — C*[*hanging the service account and access scopes for an instance .*](https://cloud.google.com/compute/docs/access/create-enable-service-accounts-for-instances#changeserviceaccountandscopes)

*Note: It’s worth noting that if the VM crashes and gets recreated, or if you adjust the cluster size, the newly generated VMs will not inherit the updated scopes.*

Solutions:

There are two potential solutions to the issue at hand:

1. [Create a new Service Account](https://www.youtube.com/watch?v=tSnzoW4RlaQ&ab_channel=GoogleCloudTech) with the necessary scope and utilize it directly within the application.
    
2. Generate a new instance with the required scopes and migrate all relevant data over to this new instance.
    

While the first approach provides greater flexibility by allowing individual pods to have their own service accounts, it requires additional management overhead. As a result, I won’t be delving into this method in this post, but it is a useful option if you require more granular control.

The second approach, on the other hand, eliminates the need for any code modifications or service account management, but it does carry the risk of downtime during the initialization/start up of the new VMs.

However, by following a few straightforward steps with Google Kubernetes Engine, it is possible to avoid this downtime altogether. Let’s delve into these steps below!

### The initial setup

For this blog post, the setup we will be discussing in this blog post involves 3-node Kubernetes cluster on Google Kubernetes Engine, supporting a service backed by a deployment with 6 replicas.

Here are the nodes:

Here are the pods (modified to fit the screen):

You can see that the pods are distributed across the nodes.

### Disaster strikes!

*Oh noo, it appears that the nodes do not have the necessary permissions!*

To rectify this, you’ll need to create fresh nodes that come with the appropriate permissions. One approach to accomplishing this is by generating a new node pool that is equivalent in size to the old pool. The new node pool can coexist alongside the old one, enabling the scheduling of new pods on it.

For instance, suppose your code needs access to the “[devstorage.read](http://devstorage.read)\_write” and “pubsub” scopes.

As always, you [can customize](https://cloud.google.com/sdk/gcloud/reference/container/node-pools/create) this command to fit your needs.

Upon inspecting the nodes, you’ll notice that three additional nodes with the new pool name have been added.

However, the pods are still on the old nodes!

### Time to drain

At this stage, you may opt to delete the old node pool. Kubernetes will recognize that the pods are no longer active and will reallocate them to the new nodes.

Nonetheless, removing the old node pool could lead to a brief downtime in the application since Kubernetes would need some time to acknowledge that the nodes are offline and initiate the relocation of containers to the new nodes. While this duration might only be a few seconds or minutes, it could be deemed unacceptable in our scenario.

A more suitable approach would be to eliminate the pods from the old nodes gradually, followed by the removal of the nodes from the cluster. Fortunately, Kubernetes provides built-in commands to perform these actions.

First, you should cordon each of the old nodes, which would prevent any new pods from being scheduled onto them.

```plaintext
$ kubectl cordon <NODE_NAME>
```

Then, drain each node. This will delete all the pods on that node.

*Caution: Ensure that your pods are managed by a ReplicaSet, Deployment, StatefulSet, or a similar entity. Standalone pods will not be rescheduled!*

```plaintext
$ kubectl drain <NODE_NAME> --force
```

After draining a node, it is important to ensure that the new pods are up and running before proceeding to the next one. After completing this process for all nodes, you can confirm that all pods are running on the new nodes!

### Delete the old pool

It’s now time to delete the old node pool. Keep in mind that you should replace “default-pool” with the name of the pool you want to delete.

Congratulations! You have successfully updated your Kubernetes cluster with new scopes/permissions without any downtime.

![](https://cdn-images-1.medium.com/max/1200/0*7ppO3eaaUcky50Hq.jpg align="left")

*Thanks for reading*💫  
If you enjoyed this article share it with your friends and colleagues. Let me know your thoughts in the comments section, and don’t forget to clap.

Follow me for more tech blogs.

[LinkedIn](https://www.linkedin.com/in/diprajghosh/) | [Instagram](https://www.instagram.com/dipraj_ghosh/) | [Facebook](https://www.facebook.com/diprajriki/)

\-Dipraj ✨