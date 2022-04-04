
# Creating a Key Pair that can be imported into AWS

```
# AWS needs RSA format
ssh-keygen -t rsa -b 4096
```

# Setting up a single key pair in multiple AWS Regions

First get a copy of your public key in RFC4716 format:
``` bash
ssh-keygen -e -m RFC4716 -f ~/.ssh/private-key.pem
```

Copy the entire output into the AWS console:
```
---- BEGIN SSH2 PUBLIC KEY ----
---- END SSH2 PUBLIC KEY ----
```
