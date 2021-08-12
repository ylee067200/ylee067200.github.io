FROM ylee/dev-basic:1

##	Needed by MDS
RUN apt install  -y \
		mtd-utils subversion patch patchutils zlib1g zlib1g-dev doxygen dmsetup \
		grunt automake rename libtool net-tools ssh-askpass rsync netpbm squashfs-tools \
		python3 python3-pip \
		luajit php-cli npm default-jdk \
		libxml-dom-perl libcurl4-openssl-dev libncurses5 libncurses5-dev \
		libpcre3-dev lib32z1 

##	Adding Python packages
RUN pip3 install --no-cache-dir --upgrade pip && \
	pip3 install --no-cache-dir sentry-sdk gitpython numpy

RUN cd /usr/bin && ln -s python3 python

