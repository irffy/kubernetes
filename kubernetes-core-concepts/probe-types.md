# Kubernetes Probes: Startup, Readiness, and Liveness

## Probe Overview

### Startup Probe
**Purpose:** Verify application has successfully started  
**When to Use:** For applications with long initialization times (e.g., loading large datasets)  
**Behavior:**
- Runs before other probes
- Container restarts on continuous failures
- Example Configuration:
```yaml
startupProbe:
  httpGet:
    path: /healthz
    port: 8080
  initialDelaySeconds: 30
  periodSeconds: 5
  failureThreshold: 5
```

### Readiness Probe
**Purpose:** Check if application can handle traffic  
**When to Use:** When application needs post-startup preparation time  
**Behavior:**
- Removes pod from service endpoints on failure
- No container restart
- Example Configuration:
```yaml
readinessProbe:
  httpGet:
    path: /ready
    port: 8080
  initialDelaySeconds: 35
  periodSeconds: 5
  failureThreshold: 3
```

### Liveness Probe
**Purpose:** Verify application is still healthy  
**When to Use:** Detect hung/crashed applications  
**Behavior:**
- Restarts container on failures
- Runs continuously
- Example Configuration:
```yaml
livenessProbe:
  httpGet:
    path: /healthz
    port: 8080
  initialDelaySeconds: 40
  periodSeconds: 10
  failureThreshold: 3
```

## Comparison Table

| Feature                | Startup Probe          | Readiness Probe           | Liveness Probe           |
|------------------------|------------------------|---------------------------|--------------------------|
| **Purpose**            | Verify startup         | Check traffic readiness   | Monitor health           |
| **Failure Action**     | Restart container      | Remove from service       | Restart container        |
| **Initial Delay**      | 30 seconds             | 35 seconds                | 40 seconds               |
| **Probe Frequency**    | 5 seconds              | 5 seconds                 | 10 seconds               |
| **Failure Threshold**  | 5 attempts             | 3 attempts                | 3 attempts               |

## Real-World Analogy
> Imagine a restaurant:
> - **Startup:** Kitchen prepped, staff ready
> - **Readiness:** Tables set, ingredients stocked
> - **Liveness:** Chefs cooking, waiters serving

## Key Takeaways
1. Use startup probes for slow-initializing applications
2. Configure readiness probes to manage traffic flow
3. Implement liveness probes for automatic crash recovery
4. Adjust timings based on actual application requirements
5. Combine probes for comprehensive health monitoring
