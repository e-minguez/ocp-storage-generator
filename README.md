# ocp-storage-generator

Basic template that creates a pod and a pvc with the required size.

## Parameters

* `NAME` - Self explanatory (ocp-storage-generator by default)
* `VOLUME_CAPACITY` - PVC size in Gi (1Gi by default)

## Usage

```
oc process -f ./template.yaml | oc create -f -
```

## Examples

In the event of requiring 2Gi of storage:

```
oc process -f ./template.yaml -p VOLUME_CAPACITY="2Gi" | oc create -f -
```


In the event of requiring 4 pods and 2Gi of storage per pod:

```
for i in $(seq 1 4); do
  oc process -f ./template.yaml \
    -p NAME="storage-generator-${i}" \
    -p VOLUME_CAPACITY="2Gi" | oc create -f -
done
```
