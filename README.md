
POC - NetworkPolicy for App and Collector case


1. Create collector-one and collector-two

kubectl apply -f collector-one.yaml -f collector-two.yaml

2. Create appx

kubectl apply -f appx.yaml 

3. test connect to collector


kubectl exec  myapp -n appx -- curl --connect-timeout 10 -s  http://collector.collector-one.svc.cluster.local:8888
kubectl exec  myapp -n appx -- curl --connect-timeout 10 -s  http://collector.collector-one.svc.cluster.local:9999

kubectl exec  myapp -n appx -- curl --connect-timeout 10 -s  http://collector.collector-two.svc.cluster.local:8888
kubectl exec  myapp -n appx -- curl --connect-timeout 10 -s  http://collector.collector-two.svc.cluster.local:9999

4. Deny all egress to all pods in appx

 kubectl apply -f 01-deny-all-egress-appx.yaml

5. repeat #3

6. allow to DNS and (port 8888 and namespace collector-one) in appx

kubectl apply -f 02-allow2coredns.yaml -f 03-allow2collector-port8888.yaml

7. report #3




















 
