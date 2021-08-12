FROM ylee/dev-basic:1

##	Install packages for OpenBMC
RUN apt install -y \
		python3 python3-pip \
		libcurl4-openssl-dev libcurlpp-dev \
		libsdl1.2-dev \
		libsystemd-dev \
		libtool autoconf-archive libpciaccess-dev meson cmake libfmt-dev

##	Install python packages
RUN pip3 install --no-cache-dir --upgrade pip && \
	pip3 install --no-cache-dir pexpect pyyaml mako

RUN cd /usr/bin && ln -s python3 python

