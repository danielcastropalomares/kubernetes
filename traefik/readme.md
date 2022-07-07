To test the access inside of cluster:

Check the Internal IP of traefik service:
```
vagrant@kubemaster:~$ kubectl get service -A | grep trae
traefik-v2    traefik                   LoadBalancer   10.97.1.155      <pending>     80:4004/TCP,443:4027/TCP   50m
```

Start a temp pod and add to hosts file the entry foo.com:

```
kubectl run temp2 --image=nginx:alpine -it --rm -- /bin/sh
echo "10.97.1.155	foo.com" >> /etc/hosts
```

Check with curl the connection:

```
/ # curl foo.com/bar/
hello to bar website
```
