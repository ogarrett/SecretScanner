---
title: SecretScanner QuickStart
---

# Quick Start

Pull the latest SecretScanner image, and use it to scan a `node:latest` container.

## Pull the latest SecretScanner image

```bash
docker pull deepfenceio/deepfence_secret_scanner:latest
```

## Scan a Container Image

Pull an image to your local repository, then scan it

```bash
docker pull node:latest

docker run -it --rm --name=deepfence-secretscanner \
	-v /var/run/docker.sock:/var/run/docker.sock \
	deepfenceio/deepfence_secret_scanner:latest \
	-image-name node:latest

docker rmi node:latest
```

## Process the results with jq

You can summarise the results by processing the JSON output, e.g. using `jq`:

```bash
docker run -it --rm --name=deepfence-yaradare \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /tmp:/home/deepfence/output \
    deepfenceio/deepfence-yaradare:latest \
    --image-name node:latest --json-filename=node-secret-scan.json

cat /tmp/node-secret-scan.json | jq '.Secrets[] | { rule: ."Matched Rule Name", file: ."Full File Name" }'
```