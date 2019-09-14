

### Simple Docker Tests

```bash
docker run hello-world
```

```bash
docker run -d -p 8081:80 nginx:alpine
curl http://127.0.0.1:8081/
```

### Logs

Watch live flow of logs on MacOs
```bash
pred='process matches ".*(ocker|vpnkit).*"
  || (process in {"taskgated-helper", "launchservicesd", "kernel"} && eventMessage contains[c] "docker")'
/usr/bin/log stream --style syslog --level=debug --color=always --predicate "$pred"
```

Last day of logs
```bash
show --debug --info --style syslog --last 1d --predicate "$pred" >/tmp/logs.txt
```

### Fix No Space Left

```bash
docker system prune -a
```