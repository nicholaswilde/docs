# Permissions

With Kubernetes, `s6-overlay` is not needed. Instead Kubernetes can use
[Security Context](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)
on either the pod or container to tell what the container should run as,
and/or what permissions files should be written as.

## Managing Permissions

There are several different methods you can use to make these containers have
write access to your file storage.

!!! note
    Our images use a default user/group id of `568`. The user and group ids
    cannot be changed at the container runtime.

### Security Contexts method

You can change the Kubernetes
[Security Contexts](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)
to allow the container to have permissions to write to your file storage.

In our [Helm charts](https://github.com/k8s-at-home/charts/) this can be accomplished
by setting the `podSecurityContext.runAsUser`, `podSecurityContext.runAsGroup`,
and `podSecurityContext.fsGroup` values to your required user / group ids.

### Direct volume method

If you can access the volume's data without the pod running. You can run
`chown -R 568:568 <path-to-your-volume>`. This step can be a bit complicated
if you are not very familiar with your storage interface.

### initContainer method

Implement a `initContainer` that runs as root to automatically chown the volume's
data. Take the following as an example.

```yaml
initContainers:
- name: update-volume-permission
  image: busybox
  command: ["sh", "-c", "chown -R 568:568 /mytest"]
  volumeMounts:
  - name: config
    mountPath: /config
  securityContext:
    runAsUser: 0
```
