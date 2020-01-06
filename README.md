Docker CI images
====

Just for CI testing:

```yaml
# Example: .gitlab-ci.yml
test:
  image: andytruong/golang:1.13
  script: go test -cover ./... -v
```
