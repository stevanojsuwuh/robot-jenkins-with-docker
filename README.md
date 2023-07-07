# Dockerfile Introduction

## Build Image

```bash
docker build -f Dockerfile -t <image-name> .
```

Keterangan:

- `-f` digunakan jika penamaan bukan `Dockerfile`

## Container Run
```bash
docker run --rm <image-name>
