FROM ubuntu:18.04

ENV LC_CTYPE C.UTF-8

# RUN dpkg --add-architecture i386

RUN echo "apt updating..."
RUN apt update
RUN echo "apt installing..."
RUN apt install -y cmake strace ltrace curl wget gcc net-tools vim gdb python python3 python3-pip wget git make procps libpcre3-dev libdb-dev libxt-dev libffi-dev libxaw7-dev python-pip rxvt-unicode-256color libssl-dev

# 32bit lib are pending
# RUN apt-get install -y libc6:i386 libncurses5:i386 libstdc++6:i386 

RUN echo "installing arm tools"
RUN apt install -y gdb-multiarch gcc-arm-none-eabi

RUN echo "installing avr development tools..."
RUN apt install -y gcc-avr avrdude binutils-avr avr-libc

# seems comflicts with peda-arm
#RUN echo "installing gef..."
#RUN (wget -q -O- https://github.com/hugsy/gef/raw/master/scripts/gef.sh | sh)

RUN echo "installing peda-arm"
RUN (git clone https://github.com/alset0326/peda-arm.git ~/peda-arm)
RUN (echo "source ~/peda-arm/peda-arm.py" >> ~/.gdbinit)

RUN echo "pip install ..."
RUN pip install capstone requests pwn r2pipe  && \
        pip3 install unicorn capstone ropper

RUN echo "installing keystone..."
WORKDIR /root
RUN cd /root &&\
        git clone https://github.com/keystone-engine/keystone.git && \
        cd keystone && \
        mkdir build && \
        cd build && \
        ../make-share.sh && \
        make install && \
        ldconfig && \
        cd ../bindings/python && \
        make install3

RUN echo "installing other tools..."
RUN cd && \
        mkdir tools && cd tools && \
        git clone https://github.com/JonathanSalwan/ROPgadget && \
        git clone https://github.com/radare/radare2 && \
        cd radare2 && sys/install.sh && \
        wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/7-2018q2/gcc-arm-none-eabi-7-2018-q2-update-linux.tar.bz2?revision=bc2c96c0-14b5-4bb4-9f18-bceb4050fee7?product=GNU%20Arm%20Embedded%20Toolchain,64-bit,,Linux,7-2018-q2-update

RUN echo "installing ruby and one-gadget"
RUN apt-get -y install ruby-full
RUN gem install one_gadget
RUN apt-get install -y tmux

