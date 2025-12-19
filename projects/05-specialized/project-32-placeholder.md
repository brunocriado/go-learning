# Project 32: Kubernetes Operator

[← Back to Specialized Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a Kubernetes operator that manages custom resources implementing the operator pattern with controllers, reconciliation loops, and event handling.

**Difficulty:** Specialized  
**Estimated Time:** 6-8 weeks  
**Prerequisites:** Projects 21, 28, Kubernetes experience

## What You'll Learn

- Kubernetes API fundamentals
- Custom Resource Definitions (CRDs)
- Controller pattern
- Reconciliation loops
- Watch and event handling
- Leader election
- Finalizers
- Admission webhooks

## Core Features

1. **Custom Resources:** Define CRD (e.g., Database, Application), validation rules, subresources
2. **Controller:** Watch for changes, reconcile state, create/update child resources
3. **Lifecycle Management:** Creation, updates, deletion with finalizers
4. **Advanced:** Leader election, admission webhooks, status conditions, events

## CRD Definition Example

```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: databases.example.com
spec:
  group: example.com
  versions:
    - name: v1
      served: true
      storage: true
      schema:
        openAPIV3Schema:
          type: object
          properties:
            spec:
              type: object
              properties:
                size: {type: string}
                version: {type: string}
            status:
              type: object
  scope: Namespaced
  names:
    plural: databases
    singular: database
    kind: Database
```

## Controller Reconciliation Pattern

```go
func (r *DatabaseReconciler) Reconcile(ctx context.Context, req ctrl.Request) (ctrl.Result, error) {
    // 1. Get desired state from custom resource
    var database examplev1.Database
    if err := r.Get(ctx, req.NamespacedName, &database); err != nil {
        return ctrl.Result{}, client.IgnoreNotFound(err)
    }
    
    // 2. Get actual state from cluster
    var deployment appsv1.Deployment
    err := r.Get(ctx, types.NamespacedName{Name: database.Name, Namespace: database.Namespace}, &deployment)
    
    // 3. Compare and determine actions
    // 4. Apply changes
    // 5. Update status
    // 6. Requeue if needed
    
    return ctrl.Result{}, nil
}
```

## Tools

- **Kubebuilder:** Project scaffolding and code generation
- **Operator SDK:** Alternative operator framework

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 32"):
- Complete CRD definitions
- Controller implementation patterns
- Reconciliation logic
- RBAC configuration
- Deployment manifests
- Testing strategies

---

[← Back to Specialized Projects](README.md) | [↑ Back to Index](../../projects-index.md)
