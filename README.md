# MariaDB Operator for Kubernetes

This is a MariaDB Operator, which makes management of MariaDB instances (or clusters) running inside Kuberenetes clusters easy. It was built with the [Operator SDK](https://github.com/operator-framework/operator-sdk) using [Ansible](https://www.ansible.com/blog/ansible-operator).

The aim of this project is help to close this issue: https://github.com/geerlingguy/mariadb-operator/issues/12

Creating the operator:

```sh
operator-sdk init --plugins=ansible --domain operator
operator-sdk create api --group mariadb --version v1 --kind MariaDB --generate-role
```
