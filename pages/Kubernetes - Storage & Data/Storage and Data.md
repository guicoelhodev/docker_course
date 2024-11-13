Kubernetes has your own volume system, check out keys differences

![kubernetesVolume](../../assets/Storage%20and%20Data1.png)

Here is a example about how create a volume inside of Pod

```yaml
spec:
  containers:
	name: story
	image: your-dockerimage
	volumeMounts:
		- mountPath: /app/story
		name: story-volume
  volumes:
	- name: story-volume
	  empyDir: {}
```

You can add volumes with controlled path access

```yml
volumes:
	- name: story-volume
	hostPath:
		path: /data
		type: DirectoryOrCreate
```

### Persistent Volumes
---

![persistentVolumes](../../assets/PersistentVolumes.png)
![persistentVolumesPV](../../assets/persistent%20volume%20PV.png)
