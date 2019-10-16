# Ansible Collection - operator_sdk.util

## Prereqs

The collection can only be created and built using Ansible 2.9+ (not
released yet). 

`pip install  git+https://github.com/ansible/ansible.git@devel`


## Creation

The default creation gives a directory for namespace, a subdir for name.
In this case, we should avoid having `operator_sdk` git repo, which
would be confusing next to `operator-sdk`.  Ansible namespaces and names
cannot have `-` in them, but this restriction does not apply to the git
repo name. Instead, I went with `operator-sdk-util`.

```
ansible-galaxy collection init operator_sdk.util
mv operator_sdk/util operator-sdk-util
rmdir operator_sdk
mkdir operator-sdk-util/plugins/modules/
wget https://raw.githubusercontent.com/fabianvf/ansible-k8s-status-module/master/k8s_status.py -O .operator-sdk-util/plugins/modules/k8s_status.py
```

## Build

`ansible-galaxy collection build`

Produces a tarball, which can be installed locally, or published to
Ansible galaxy. We probably don't want to keep this in git, but for now
I've included it for the demo.

## Local Install

`ansible-galaxy collection install operator_sdk-util-1.0.0.tar.gz -p ~/.ansible/collections`

## Publish

The result can be published to Ansbile galaxy but we will need to create
a namespace.
https://galaxy.ansible.com/docs/contributing/namespaces.html#requesting-additional-namespaces

`ansible-galaxy collection publish operator_sdk-util-1.0.0.tar.gz`

