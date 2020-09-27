# MariaDB Operator for Kubernetes

This is a MariaDB Operator, which makes management of MariaDB instances (or clusters) running inside Kuberenetes clusters easy. It was built with the [Operator SDK](https://github.com/operator-framework/operator-sdk) using [Ansible](https://www.ansible.com/blog/ansible-operator).

The aim of this project is help to close this issue: https://github.com/geerlingguy/mariadb-operator/issues/12

Creating the operator:

```sh
operator-sdk init --plugins=ansible --domain operator
operator-sdk create api --group mariadb --version v1 --kind MariaDB --generate-role
```

To connect to the mariadb Database run:

```sh
POD=`kubectl get pods -n mariadb-operator -l app=mariadb | grep Running | grep 1/1 | awk '{print $1}'`
kubectl exec -n mariadb-operator -it $POD -- mysql -uroot -ppassword
```

Build the operator

```sh
make docker-build docker-push IMG=imjoseangel/mariadb-operator:v1.0.0
```

Deploy de operator

```sh
make install
make deploy IMG=imjoseangel/mariadb-operator:v1.0.0
```

Verify status:

```sh
kubectl get deployment -n mariadb-operator-system

NAME                                  READY   UP-TO-DATE   AVAILABLE   AGE
mariadb-operator-controller-manager   1/1     1            1           8s
```

View the Ansible Logs:

```sh
kubectl logs deployment/mariadb-operator-controller-manager -n mariadb-operator-system manager -f
```

Deploy MariaDB

```sh
kubectl apply -f config/samples/mariadb_v1_mariadb.yaml
```
