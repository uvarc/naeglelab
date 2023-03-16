# naeglelab
naeglelab


# seal secrets
vi secrets.yaml 

paste the following 
-------------------
apiVersion: v1
kind: Secret
metadata:
  name: proteome-scout-3-secrets
data:
  CELERY_ACCESS_KEY: <echo value | base64>
  CELERY_BROKER_URL: <echo value | base64>
  CELERY_RESULT_BACKEND: <echo value | base64>
  CELERY_SECRET_ACCESS_KEY: <echo value | base64>
  DATABASE_URL: <echo value | base64>
  QUEUE_URL: <echo value | base64>
--------------------

cat secret.yaml | kubeseal --controller-namespace=kube-system --format yaml --cert ssz-k8-sealed-secret-cert.pem > sealedsecret.yaml 

copy just the ecrypted data section to respective section in templates/proteome-scout-3-sealed-secrets.yaml
Note: find ssz-k8-sealed-secret-cert.pem in ssz-projects git repo applicable only for sealing secrets for projects hosted on ssz k8 env