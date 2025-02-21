# Swagger UI Kubernetes Deployment

This repository contains the Kubernetes manifests required to deploy Swagger UI in a Kubernetes cluster using a **StatefulSet** and **ALB Ingress Controller**.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Deployment](#deployment)
- [Fetching OpenAPI JSON from API Gateway](#fetching-openapi-json-from-api-gateway)
- [Uploading OpenAPI JSON to S3](#uploading-openapi-json-to-s3)
- [Serving OpenAPI JSON via CloudFront](#serving-openapi-json-via-cloudfront)
- [Configuring Swagger UI](#configuring-swagger-ui)

---

## Prerequisites

- A running **Kubernetes cluster** with `kubectl` configured
- **AWS CLI** installed and configured
- **Helm** installed (for managing ingress controllers if needed)
- **ALB Ingress Controller** installed in your Kubernetes cluster

## Deployment

To deploy Swagger UI, apply the following Kubernetes manifests in order:

```sh
kubectl apply -f configmap.yaml
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
kubectl apply -f service.yaml
kubectl apply -f statefulset.yaml
kubectl apply -f ingress.yaml
```

After deployment, Swagger UI should be accessible at `https://swagger.example.com` (or your configured hostname).


## Uploading OpenAPI JSON to S3

If your S3 bucket is **publicly accessible**, you can directly reference the file from there. If it's **private**, you'll need to use CloudFront.

### Uploading to S3

1. Upload the file to an S3 bucket (`your-bucket-name`):

2. Make the file public (if allowed):


   https://your-bucket-name.s3.amazonaws.com/swagger.json


## Configuring Swagger UI

After updating the ConfigMap, restart the Swagger UI pod for changes to take effect:


kubectl delete pod -l app=swagger-ui -n swagger-ui

---

## Conclusion

By following these steps, you've successfully:

1. Deployed Swagger UI on Kubernetes
2. Retrieved OpenAPI JSON from API Gateway
3. Uploaded it to an S3 bucket
4. Configured CloudFront to securely serve the JSON file
5. Updated Swagger UI to use the CloudFront URL

Your Swagger UI is now fully operational with a secure API definition reference!

