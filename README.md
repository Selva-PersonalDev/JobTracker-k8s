Pause and scale the App to 0 :
******************************
kubectl scale deployment jobtracker-core --replicas=0 -n jobtracker && \
kubectl delete svc jobtracker-core -n jobtracker && \
gcloud container clusters resize jobtracker-gke --node-pool primary-pool --num-nodes=0 --region us-central1
kubectl get nodes                (To Confirm no nodes running)
kubectl get pods -n jobtracker   (To Confirm no pods running)

-----------------------------------------------------------------------------------------------
Start the app :
***************
gcloud container clusters resize jobtracker-gke --node-pool default-pool --num-nodes=1 --region us-central1 && \
kubectl get nodes    (To verify node created)
kubectl apply -f JobTracker-k8s/ && \
kubectl scale deployment jobtracker-core --replicas=1 -n jobtracker   (Optional)
kubectl rollout restart deployment jobtracker-core -n jobtracker
kubectl get svc -n jobtracker  (To Get external IP)

----------------------------------------------------------------------------------------------------