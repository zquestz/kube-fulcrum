# kube-fulcrum

Kubernetes configurations for Fulcrum on GCE.

## Deployment

1. Add a new blank disk on GCE called `fulcrum-data` that is 100GB.
2. Update `main.conf` with your hostname, bitcoind credentials and any custom settings.
3. Base64 encode `main.conf`, and paste it in `kube/fulcrum-secrets.yml`.
4. Run `kubectl apply -f kube/fulcrum-certs-job.yml` to setup your self signed cert.
5. Run `kubectl apply -f kube/fulcrum-secrets.yml` to deploy your Fulcrum configuration.
6. Run `kubectl apply -f kube/fulcrum-deployment.yml` to deploy Fulcrum. Make sure the logs look okay.
7. Deploy the required services, the only required service is `fulcrum-srv.yml`.

```sh
  kubectl apply -f kube/fulcrum-admin-srv.yml
  kubectl apply -f kube/fulcrum-stats-srv.yml
  kubectl apply -f kube/fulcrum-srv.yml
```
