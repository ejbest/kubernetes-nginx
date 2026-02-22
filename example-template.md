<pre>
apiVersion: v1                    → Resource type (Pod in this case)
kind: Pod                          → Unique name for the Pod
metadata:
  name: techops-pod                → To organize and select Pods
  labels:
    app: techops                   → App label, useful for selectors
    tier: backend                  → To identify the application layer

spec:
  containers:
  - name: techops-container        → Container(s) running in this Pod
    image: nginx:1.23              → Name of the container
    ports:
    - containerPort: 80            → Docker image for the container
    env:
    - name: ENV                    → Port the container exposes internally
      value: production             → Environment variables for configuration
  volumeMounts:
  - name: config-volume            → Volumes mounted inside the container
    mountPath: /usr/share/nginx/html → Volume defined in the "volumes" section
                                     → Mount point inside the container

  volumes:
    - name: config-volume          → Name of the volume
      configMap:
        name: techops-config       → Use ConfigMap as the source
      restartPolicy: Always        → Reference the ConfigMap named "techops-config"
      
  nodeSelector:
    disktype: ssd                  → Pod restart policy (Always, OnFailure, or Never)
  tolerations:
    - key: "special-taint"         → Schedule pod on specific nodes
      operator: "Equal"            → Schedule only on nodes labeled with "disktype=ssd"
      value: "true"                → Allows scheduling on tainted nodes
      effect: "NoExecute"          → Taint key to tolerate (exec match) or Exists
                                   → Value to match
                                   → Effect: NoSchedule (can't schedule), NoExecute (evict)

  securityContext:
    runAsUser: 1000                → Pod-level security settings
    runAsGroup: 3000               → Run containers as user ID
    fsGroup: 2000                  → Run containers with this group ID
                                   → Group ownership for mounted volumes



  initContainers:
  - name: init-techops             → Runs before the main containers
    image: busybox                 → Init container name
    command: ["sh", "-c", "echo Init; sleep 5"] → Image for the init container
                                              → Setup commands


</pre>
