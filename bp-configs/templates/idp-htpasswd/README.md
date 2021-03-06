# Configure `htpasswd` Identity Provider (idp)

- Create `users.htpasswd` file wih users and passwords

```bash
# example
htpasswd -c -B -b users.htpasswd telcoadmin Redhat01
htpasswd    -B -b users.htpasswd operations Redhat01
htpasswd    -B -b users.htpasswd vendorcnf1 Redhat01
htpasswd    -B -b users.htpasswd vendorcnf2 Redhat01
htpasswd    -B -b users.htpasswd vendorcnf3 Redhat01
```

- Create secret

```bash
# Create into cluster
oc create secret generic idp-htpass-secret --from-file=htpasswd=users.htpasswd -n openshift-config

# Create to file
oc create secret generic idp-htpass-secret --from-file=htpasswd=users.htpasswd -n openshift-config --dry-run=client -o yaml > 01-htpasswd-secret-example.yaml
```

- To designate a user as `cluster-admin`

```bash
oc adm policy add-cluster-role-to-user cluster-admin telcoadmin
```

## Removing default `kubeadmin` user

```bash
oc delete secrets kubeadmin -n kube-system
```
