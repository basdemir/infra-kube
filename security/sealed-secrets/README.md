###  How can I do a backup of my SealedSecrets?
If you do want to make a backup of the encryption private keys, it's easy to do from an account with suitable access and:

```bash
kubectl get secret -n kube-system -l sealedsecrets.bitnami.com/sealed-secrets-key -o yaml > master.key
```
NOTE: This file will contains the controller's public + private keys and should be kept omg-safe!

To restore from a backup after some disaster, just put that secrets back before starting the controller - or if the controller was already started, replace the newly-created secrets and restart the controller:

```bash
kubectl apply -f master.key
kubectl delete pod -n kube-system -l name=sealed-secrets-controller
```

### Can I decrypt my secrets offline with a backup key?
If you have backed up one or more of your private keys (see previous question), you can use the kubeseal --recovery-unseal --recovery-private-key file1.key,file2.key,... command to decrypt a sealed secrets file.

```bash
kubeseal --recovery-unseal --recovery-private-key master.key < dnmoutsecret.json
```

### Can I bring my own (pre-generated) certificates?

Yes, you can provide the controller with your own certificates so it will consume them.
Please check [here](https://github.com/bitnami-labs/sealed-secrets/blob/main/docs/bring-your-own-certificates.md) for a workaround.
