# kube-scheduler
## Role
Assign pods to nodes

## Operation Mode
Controller Loop

## Operation Flow

```mermaid
flowchart TD

G((Start))--> A

A[Get list of Pods where `spec.nodeName` is empty] -->

B{Any unscheduled pods?} --> |No| G

B --> |Yes| C[Get list of Nodes] --> F

subgraph F[For each unscheduled pod]

    D[Score Nodes based on Pod scheduling constraints] --> E(Patch Pod's `spec.nodeName` to highest scoring Node's `metadata.name`)

end

F --> G
```

## Input Resources
- [Pod](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/)
- [Node](https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/node-v1/)
## Output Resources
_None_

## Dependencies
- [kube-api-server](kube-api-server.md)

## Inbound communication
- `/metrics`
## Outbound communications
- [kube-api-server](kube-api-server.md)