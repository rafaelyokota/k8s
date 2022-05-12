

Install Kind
     <https://kind.sigs.k8s.io/>
Install kubetcl
    <https://kubernetes.io/docs/tasks/tools/>
     <https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/>

to Create Cluster local
kind create cluster --name my-cluster

to Create Cluster local from yml
kind create cluster --config=kind.yml --name=k8s-developement

List Cluster
kubectl config get-clusters

Change Context to Cluster
kubectl config use-context kind-k8s-developement

kubectl apply -f config.yaml
kubectl port-forward pod/goserver 8000:80
kubectl get pods
kubectl get replicasets

kubectl describe pod goserver-8cgjg

kubectl delete pod goserver
kubectl delete replicasets goserver

O Problema do Replicaset
 caso vc atualize a versao do a imagem do template da imagem para outras versão
 tem que matar pod por pod para atualizar(inviavel)

Deployments > Replicasets > Pods

Rollback e Revisões

kubectl rollout history deployment goserver //lista versoes de deployments
kubectl rollout undo deployments goserver // volta pra anterior
kubectl rollout undo deployments goserver --to-revision=1(numero da revisão)





repositorio dentro do k8s
<https://www.linuxtechi.com/setup-private-docker-registry-kubernetes/>


Conceito de Services
    Como acessar essa aplicação? qual pod esse cliente vai acessar? pod não quer dizer que precisa e pode ser acessada.

Service é a porta de entrada para app.
    quer acessar API XPTO -> (10 replicas do pod), atua como loadbalance.
    kubectl port-forward pod/goserver 8000:80 por exemplo caso precise de acesso, temporario, no dia dia é inviavel, e não pratico.

    kubectl apply -f service.yml
    kubectl get svc

    Service ja trabalha com resolução de dns, exemplo 
        root:root@goserver-service  (suponhamos que servico seja de mysql)

    expoe a porta externa 8000 para o service 
    kubectl port-forward svc/goserver-service 8000:80