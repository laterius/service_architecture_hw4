1. kubectl apply -f namespaces.yaml
#Разворачиваем Istio
2. istioctl install --set profile=demo -y
3. kubectl apply -f istio/disable-mtls.yaml
#Разворачиваем kiali
3. helm repo add kiali https://kiali.org/helm-charts
   helm repo update
   helm install -n kiali-operator kiali-operator kiali/kiali-operator
   kubectl apply -f kiali/kiali.yaml
**alternative**: kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.15/samples/addons/kiali.yaml
#Ставим прометеус
4. kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.15/samples/addons/prometheus.yaml
5. kubectl apply -f manifests
6. kubectl -n istio-system get services
   istio-egressgateway    ClusterIP      10.99.62.218     <none>          80/TCP,443/TCP                                                               2m13s
   istio-ingressgateway   LoadBalancer   10.101.39.126    10.101.39.126   15021:31684/TCP,80:31430/TCP,443:31405/TCP,31400:32066/TCP,15443:32169/TCP   2m13s
   istiod                 ClusterIP      10.111.225.17    <none>          15010/TCP,15012/TCP,443/TCP,15014/TCP                                        2m27s
   kiali                  ClusterIP      10.104.131.115   <none>          20001/TCP,9090/TCP                                                           53s
   prometheus             ClusterIP      10.104.218.132   <none>          9090/TCP                                                                     80s
7. istioctl dashboard kiali
