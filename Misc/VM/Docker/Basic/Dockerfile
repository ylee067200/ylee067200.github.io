FROM ubuntu:latest

##	Setting timezone to avoid docker image build be freezed by configuring timezone
RUN ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime

##	Insert tools and libraries we need for developing
RUN apt update && \
	apt install -y bc tzdata vim tree rename cifs-utils sudo iproute2 locales iputils-ping \
		chrpath diffstat unzip socat cpio xz-utils tar \
		openssh-server curl wget \
		git git-core git-doc \
		build-essential libc++-dev gcc-multilib cppcheck \
		gawk bison flex libncurses-dev texinfo \
		global tmux \
		apt-utils && \
	apt autoremove -y

##	Uisng bash as default shell
RUN echo "dash dash/sh boolean false" | debconf-set-selections && DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash

##	Setting locate for UTF8 environment
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

##      Adding user
RUN mkdir /var/run/sshd

##	Setting up SSH Server: Login in as root with password TesT_1234
RUN echo 'root:0penBmc' | chpasswd

RUN sed -i 's/#\?PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
	sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd

RUN echo 'export NOTVISIBLE="in users profile"' >> ~/.bashrc && \
	echo "export VISIBLE=now" >> /etc/profile

##	Export SSH Port
EXPOSE 22

##	Eunninb ssh server
CMD ["/usr/sbin/sshd", "-D"]

