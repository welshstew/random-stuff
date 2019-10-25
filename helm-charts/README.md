Setup helm on minikube

```
kubectl create -f cluster-role.yml

kubectl create serviceaccount -n kube-system tiller
kubectl create clusterrolebinding tiller-cluster-role --clusterrole=cluster-admin --serviceaccount=kube-system:tiller

helm init --service-account tiller
kubectl --namespace kube-system get pods | grep tiller


helm install --name example ./artifactory-ingest --set service.type=NodePort
```


https://hub.docker.com/r/mattgruter/artifactory

run some sample nginx container....

	

Create pvs on minikube for artifactory to use:

```

kubectl create -f pv/pvs.yml


    volumeClaimTemplates:
    - metadata:
        name:  {{ .Values.main.name }}
      spec:
        accessModes: [ "ReadWriteOnce" ]
        resoucres:
          requests:
            storage: 1Gi
```

Required secrets:

- java-certs : has cacerts
- nginx-certs: has ca.crt, server.crt, server.key (self signed for certificate based auth)
- ca-bundle: has ca-certificates.crt


