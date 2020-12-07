# helm3常用命令

### 预安装查看配置详细信息

```text
[root@localhost logs]# helm upgrade loki ./loki-stack --dry-run -n kube-mon
```

### 查看版本以及回滚

```text
# 版本查看
[root@localhost logs]#  helm hist loki -n kube-mon
REVISION        UPDATED                         STATUS          CHART                   APP VERSION     DESCRIPTION     
1               Wed Nov  4 15:29:11 2020        superseded      loki-stack-2.0.0        v2.0.0          Install complete
2               Wed Dec  2 16:34:56 2020        deployed        loki-stack-2.0.0        v2.0.0          Upgrade complete
# 版本回滚(这里是回到第一个版本)
[root@localhost logs]#  helm rollback --debug loki 1 -n kube-mon
rollback.go:61: [debug] preparing rollback of loki
rollback.go:109: [debug] rolling back loki (current: v2, target: v1)
rollback.go:68: [debug] creating rolled back release for loki
rollback.go:74: [debug] performing rollback of loki
client.go:173: [debug] checking 20 resources for changes
client.go:436: [debug] Looks like there are no changes for ServiceAccount "loki"
client.go:436: [debug] Looks like there are no changes for ServiceAccount "loki-promtail"
client.go:436: [debug] Looks like there are no changes for Secret "loki"
client.go:436: [debug] Looks like there are no changes for ConfigMap "loki-loki-stack"
client.go:436: [debug] Looks like there are no changes for ConfigMap "loki-loki-stack-test"
client.go:436: [debug] Looks like there are no changes for ClusterRole "loki-promtail-clusterrole"
client.go:436: [debug] Looks like there are no changes for ClusterRoleBinding "loki-promtail-clusterrolebinding"
client.go:436: [debug] Looks like there are no changes for Role "loki"
client.go:436: [debug] Looks like there are no changes for Role "loki-promtail"
client.go:436: [debug] Looks like there are no changes for RoleBinding "loki"
client.go:436: [debug] Looks like there are no changes for RoleBinding "loki-promtail"
client.go:436: [debug] Looks like there are no changes for Service "loki-headless"
client.go:436: [debug] Looks like there are no changes for Service "loki"
client.go:436: [debug] Looks like there are no changes for Service "loki-promtail-headless"
client.go:436: [debug] Looks like there are no changes for ServiceMonitor "loki-promtail"
rollback.go:220: [debug] superseding previous deployment 2
rollback.go:80: [debug] updating status for rolled back release for loki
Rollback was a success! Happy Helming!

```

