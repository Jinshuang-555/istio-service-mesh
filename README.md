# istio-service-mesh
This is the repo for setting up service mesh with Let's-Encrypt certificate secured Ingress Gateway using Istio and cert-manager

## setup istio service mesh ingress gateway and virtual service: 

export PATH=/Users/niujinshuang/downloads/istio-1.17.2/bin:$PATH 

istioctl install --set profile=demo -y

kubectl apply -f istio-gateway.yaml

kubectl label namespace istio-system istio-injection=enabled
kubectl label namespace default istio-injection=enabled

kubectl apply -f virtual-service.yaml

kubectl get svc istio-ingressgateway -n istio-system 

** update route53 record for istio.k8s.csye6225jinshuang.me with CNAME pointing to ELB record **


## install cert-manager: 

kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.yaml

kubectl apply -f letsencrypt-prod-issuer.yaml
kubectl apply -f certificate.yaml

