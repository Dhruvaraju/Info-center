- For terraform to work install gcloud sdk
- Then authorize it to login after completion
- To use terraform scripts run `gcloud auth application-default login`

https://www.fairwinds.com/blog/how-to-use-terraform-with-gke-a-step-by-step-guide-to-deploying-your-first-cluster

```
gcloud container clusters get-credentials gke-example --region us-central1
Fetching cluster endpoint and auth data.
kubeconfig entry generated for gke-example.
```

```
https://fig.io/manual/gcloud/container/clusters/get-credentials
```

https://cloud.google.com/sdk/gcloud/reference/container/clusters/get-credentials