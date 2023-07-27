# How to test the Must Gather Operator locally 

## Download a single node Open Shift cluster (CRC)

You can download one for free from https://console.redhat.com/openshift/create/local

Install CRC by running:

```bash
crc setup
crc start
```

You will be asked for a pull secret, you can get it from the same Red Hat page where you downloaded the package.

## Login to the cluster

For installing the operator you will need administrative privileges. You need to display and login with the `kubeadmin` user as follows:

```bash
crc console --credentials
```

Login as an admin (second line)

## Install prerequisites 

Clone and repository and install the prerequisites:

```bash
git clone https://github.com/openshift/must-gather-operator.git
cd must-gather-operator/examples/other_resources
oc apply -f .
```

Those are the namespace, service account and some RBAC permissions that allow you to run the examples.

## Install the operator

```bash
# After you clone the repo
cd must-gather-operator
oc apply -f deploy/crds/managed.openshift.io_mustgathers.yaml # needs updating on the upstream
oc -n openshift-must-gather-operator apply -f deploy # also needs updating on the upstream
```

## Build and push the operator with changes

```bash
make docker-build # did not work on macOS with ARM architecture but worked on AMD64 Linux
```

