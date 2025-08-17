# k8s-demo

## build image and send to docker hub
sudo usermod -aG docker $USER
docker login
docker image build -t renebod/fastapi:v2 .
docker push renebod/fastapi:v2

## install rke2
curl -sfL https://get.rke2.io | sudo sh -
systemctl enable rke2-server.service
systemctl start rke2-server.service
journalctl -u rke2-server -f

alias k='sudo /var/lib/rancher/rke2/bin/kubectl --kubeconfig /etc/rancher/rke2/rke2.yaml'
alias k9s='sudo k9s --kubeconfig /etc/rancher/rke2/rke2.yaml'

k -n kitchensink apply -f kubernetes.yaml
k -n kitchensink logs -f --selector app=fastapi