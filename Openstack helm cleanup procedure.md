# OpenstackHelm Cleanup Procedure

helm delete ${RELEASE_NAME} --purge

helm install ${RELEASE_NAME} --set manifests.job_db_drop=true
for NS in openstack ceph; do
done

kubectl delete namespace openstack

kubectl delete namespace ceph

sudo systemctl disable kubelet --now

sudo systemctl stop kubelet

sudo docker ps -aq | xargs -L1 -P16 sudo docker rm -f

sudo rm -rf /var/lib/openstack-helm

sudo rm -rf /var/lib/nova

For logs

POD LOGS
export POD_NAME=$(kubectl get pods --all-namespaces -o go-template --template '{{range.items}}{{.metadata.name}}{{"\n"}}{{end}}' | grep nova-cell-setup-xbsx9)

kubectl logs --namespace=openstack $POD_NAME
