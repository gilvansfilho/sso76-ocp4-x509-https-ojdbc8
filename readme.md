Login no cluster

```
$ oc login -u kubeadmin -p password https://openshift.example.com:6443
```

Importar o image stream

```
$ oc -n openshift import-image rh-sso-7/sso76-openshift-rhel8:7.6 --from=registry.redhat.io/rh-sso-7/sso76-openshift-rhel8:7.6 --confirm
```

Criar o namespace
```
oc new-project sso76
```

Adicionar a role view para o SA default
```
oc policy add-role-to-user view system:serviceaccount:$(oc project -q):default
```

criar configmap para o cli
```
oc create cm ssoextensionscli --from-file=sso-extensions.cli
```

criar secret oracle
```
oc create secret generic oracle-db-secret --from-literal=DB_JDBC_URL=external-oracle-url-db --from-literal=DB_USERNAME=oracle-db-username --from-literal=DB_PASSWORD=oracle-db-password
```

deploy do sso76

```
oc create -f sso76-ocp4-x509-https-ojdbc8.json
```