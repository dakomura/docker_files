
## docker image for pathological image analysis

###  To build image
```
docker build -t [[tag]] --no-cache .
```
You should add `no-cache` option for the first time to ensure `apt-get update -y` is properly executed.

### To run image
```
nvidia-docker run -itd --privileged -v [[VOLUME]]:[[VOLUME]] -p [[PORT]]:[[PORT]] --restart=always --name [[NAME_OF_CONTAINER]] -h ravana_docker gpat_deep
```
- It is useful to add your working directory in option `-v`, 
- If you use nvidia-docker-compose, It should be more clean.

### Discription

- username: gpat
- initial password: ishikawa

- Python=3.6 is installed by anaconda3-4.3.0 with pyenv. and Following library is installed
    - chainer
    - openslide


