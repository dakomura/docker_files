FROM nvidia/cuda:8.0-cudnn6-devel

RUN \
 apt-get update -y && \
 apt-get upgrade -y && \
 apt-get install -y build-essential && \
 apt-get install -y software-properties-common

RUN apt-get update -y

RUN apt-get install -y sudo tree openssh-server tmux curl git htop man unzip vim wget zsh libssl-dev openssl zlib1g-dev sqlite3 libgtk2.0-0

# openslide
RUN apt-get install -y libopenslide0

# for sshd
RUN sed -i 's/.*session.*required.*pam_loginuid.so.*/session optional pam_loginuid.so/g' /etc/pam.d/sshd
RUN mkdir /var/run/sshd

# create user gpat_dev
RUN useradd -m gpat \
    && echo "gpat ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
    && echo 'gpat:ishikawa' | chpasswd
RUN chsh -s /usr/bin/zsh gpat

# locale
RUN apt-get -y install locales
RUN locale-gen en_US.UTF-8

# user
USER gpat
WORKDIR /home/gpat
ENV HOME /home/gpat
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# Python (pyenv)
RUN git clone https://github.com/yyuu/pyenv.git ~/.pyenv
RUN ~/.pyenv/bin/pyenv install anaconda3-4.3.0
RUN ~/.pyenv/bin/pyenv global anaconda3-4.3.0

# pip
RUN /home/gpat/.pyenv/shims/pip install chainer
RUN /home/gpat/.pyenv/shims/pip install cupy
RUN /home/gpat/.pyenv/shims/pip install openslide-python

# conda
RUN /home/gpat/.pyenv/shims/conda install -c menpo opencv3

# volumes
RUN mkdir /home/gpat/work_space/

# for ssh
USER root
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
