# Container to run mkdocs

## About

Small docker image to run mkdocs and expose local content on a small HTTP server.

MkDocs is a fast, simple static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file. Start by reading the introduction below, then check the User Guide for more info.

## Usage

### Docker usage

- Build your own mkdocs configuration in your `mkdocs.yml`
- Mount the folder where your mkdocs.yml and all your content reside as a volume into /docs:
- Start development server on `localhost:8000`

```shell
$ docker run --rm -it -p 8000:8000 -v ${PWD}:/docs titom73/mkdocs
...
```

- Build documentation

```shell
$ docker run --rm -it -v ${PWD}:/docs titom73/mkdocs build
...
```

### Docker compose for development

Use docker-compose to override `ENTRYPOINT` and `CMD` commands:

- Install specific requirements
- Serve content on port 8000

```yaml
version: "3"
services:
  webdoc:
    image: titom73/mkdocs
    volumes:
      - ${PWD}:/docs
    entrypoint: ""
    command: ["sh", "-c", "pip install -r my/path/to/requirements.txt\
        && mkdocs serve --dev-addr=0.0.0.0:8000"]
```

## Build image

- Build local image

```shell
$ docker build --rm --pull -t titom73/mkdocs .
Sending build context to Docker daemon  3.584kB
Step 1/9 : FROM python:3.8-alpine
3.8-alpine: Pulling from library/python
Digest: sha256:c5623df482648cacece4f9652a0ae04b51576c93773ccd43ad459e2a195906dd
```

- Check build result:

```shell
$ docker images titom73/mkdocs
REPOSITORY           TAG                 IMAGE ID            CREATED             SIZE
titom73/mkdocs        latest        87f3bedeca0e        2 hours ago         168MB
```
