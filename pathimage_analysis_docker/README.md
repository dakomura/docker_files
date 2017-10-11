
## docker image for pathological image analysis

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

```
export PATH=/usr/local/nvidia/bin:/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/nvidia/lib:/usr/local/nvidia/lib64:$LD_LIBRARY_PATH
export LIBRARY_PATH=/usr/local/cuda/lib64/stubs:$LIBRARY_PATH
```


- username: gpat
- initial password: ishikawa

