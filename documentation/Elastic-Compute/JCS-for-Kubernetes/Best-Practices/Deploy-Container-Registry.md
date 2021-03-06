# Integrate with Container Registry  

See [Help documentation of Container Registry](https://docs.jdcloud.com/en/container-registry/create-image) for use method of Container Registry. For example, the registry is myregistry, the repository is myrepo, the image version number is latest and the region is cn-north-1. Users can make the alternation depending on specific conditions.  
1.   
**Step 1: Save secret all at once with time validity**
```
kubectl create secret docker-registry my-secret --docker-server=myregistry-cn-north-1.jcr.service.jdcloud.com --docker-username=jdcloud --docker-password=C********u --docker-email=l****@jd.com
```
**Step 2: Automatically obtain Token on a regular basis, long-term valid:**  
Create a jcr-credential-rbac.yaml file with the following contents:
```
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: jcr-credential-rbac
subjects:
  - kind: ServiceAccount
    # Reference to upper's `metadata.name`
    name: default
    # Reference to upper's `metadata.namespace`
    namespace: default
roleRef:
  kind: ClusterRole
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
```
Create a jcr-credential-cron.yaml file and set to obtain Token every hour. Please add JDCLOUD_ACCESS_KEY and JDCLOUD_SECRET_KEY content when using it. The content of yaml is as follows:
```
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: jdcloud-jcr-credential-cron
spec:
  schedule: "0 */1 * * *" # 0 represents the integral point of each hour. You can modify the time according to your demands. If such number is changed to 15, it means that the token will be gotten at the 15th minute per hour.
  successfulJobsHistoryLimit: 2
  failedJobsHistoryLimit: 2  
  jobTemplate:
    spec:
      backoffLimit: 4
      template:
        spec:
          serviceAccountName: default
          terminationGracePeriodSeconds: 0
          restartPolicy: Never
          hostNetwork: true
          containers:
          - name: jcr-token-refresher
            imagePullPolicy: Always
            image: jdcloudcli/jdcloud-cli:latest
            command:
            - "/bin/sh"
            - "-c"
            - |
              REGISTRY_NAME=myregistry
              JCR_REGION=cn-north-1
              DOCKER_REGISTRY_SERVER=https://${REGISTRY_NAME}-${JCR_REGION}.jcr.service.jdcloud.com
              DOCKER_USER=jdcloud
              JDCLOUD_ACCESS_KEY=****************************
              JDCLOUD_SECRET_KEY=****************************
              jdc configure add --profile ${DOCKER_USER} --access-key ${JDCLOUD_ACCESS_KEY} --secret-key ${JDCLOUD_SECRET_KEY}
              PRECHECK=`jdc cr get-authorization-token --region-id ${JCR_REGION} --registry-name ${REGISTRY_NAME} |jq .result.authorizationToken`
              if [ 'null' = "$PRECHECK" ]; then
                  echo "jdc cr call failed no valid content" 
                  exit 0 
              else
                  echo "jdc cr call return authentication string"
              fi;
              DOCKER_PASSWORD=`echo ${PRECHECK} | base64 -d |cut  -d  ':' -f2`
              kubectl delete secret my-secret || true
              echo "0:"$PRECHECK
              echo "1:"$DOCKER_REGISTRY_SERVER
              echo "2:"$DOCKER_USER
              echo "3:"$DOCKER_PASSWORD
              kubectl create secret docker-registry my-secret \
              --docker-server=$DOCKER_REGISTRY_SERVER \
              --docker-username=$DOCKER_USER \
              --docker-password=$DOCKER_PASSWORD \
              --docker-email=**@jd.com
              kubectl patch serviceaccount default  -p '{"imagePullSecrets":[{"name":"my-secret"}]}' # kubectl patch  $SERVICEACCOUNT xxxxx  -n $NAMESPACEOFSERVICEACCOUNT

```
```
kubectl apply  -f  jcr-credential-rbac.yaml
kubectl apply  -f  jcr-credential-cron.yaml
```
2. Create a yaml file with the file name of registrysecret
```
apiVersion: v1
 kind: ReplicationController
 metadata:
    name: webapp
 spec:
    replicas: 1
    selector:
      name: container-private-repo
    template:
      metadata:
        labels:
           name: container-private-repo
      spec:
        containers:
          - name:  mycontainer
            image: myregistry-cn-north-1.jcr.service.jdcloud.com/myrepo:latest
            imagePullPolicy: Always
        imagePullSecrets:
          - name: my-secret
```
3.   Create:  
 `kubectl create -f registrysecret`  
4.   View details:  
 `kubectl describe rc webapp`  
