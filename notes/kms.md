
### Decrypt a file

```
aws --region us-east-1 kms decrypt --ciphertext-blob fileb://<(echo "$1" | base64 -D ) --output text --query Plaintext | base64 -    D && echo
```