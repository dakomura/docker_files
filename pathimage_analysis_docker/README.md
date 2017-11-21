
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

Python is installed by anaconda3-4.3.0 with pyenv.
So you have to modify your rc file
```
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

Following library is installed
- chainer
- openslide

To use chainer with GPU, you have to write following lines in your .rc file.
(may not be needed)
```
export PATH=/usr/local/nvidia/bin:/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/nvidia/lib:/usr/local/nvidia/lib64:$LD_LIBRARY_PATH
export LIBRARY_PATH=/usr/local/cuda/lib64/stubs:$LIBRARY_PATH
```

- username: gpat
- initial password: ishikawa

