#Issue 1: repo not installed
	
	Solution: 
	$ cd ~
	$ mkdir bin
	$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
	$ chmod a+x ~/bin/repo
	$ export PATH="~/bin:$PATH"

#Issue 2: Need to install python 3.5+

	Solution: 	Refer the webpage//
	http://devopspy.com/python/install-python-3-6-ubuntu-lts/
			or
		Install manually-Download and configure////
	$ wget https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tgz
	$ tar -xvf Python-3.6.3.tgz
	$ cd Python-3.6.3
	$ sudo ./configure --enable-optimizations
	$ sudo make -j6
	$ sudo make install
		Verification///
	$ python3.6
	Python 3.6.3 (default, Oct  6 2017, 08:44:35)
	[GCC 5.4.0 20160609] on linux
	Type "help", "copyright", "credits" or "license" for more information.
	>>>


#Issue 3: Missing JDK or not version 1.7

	Solution: $ sudo apt-get install openjdk-7-jdk


#Issue 4: Missing Dependencies

	Solution:
	$ sudo apt-get update
	$ sudo apt-get install device-tree-compiler lzma lzop libcurl4-gnutls-dev:amd64 libc6:i386 libncurses5:i386 libstdc++6:i386 zlib1g:i386


#Issue 5: ERROR: cannot verify releases.linaro.org's certificate, issued by ‘/C=US/O=Let's Encrypt/CN=R3’:
	Issued certificate has expired.
	To connect to releases.linaro.org insecurely, use `--no-check-certificate'.

	Solution:
	~/marsh-6.0$ cd cd ti-kernel/scripts/
	~/marsh-6.0/ti-kernel/scripts$ vim gcc.sh
	Modify line no. 43 to WGET="wget -c --directory-prefix=${gcc_dir}/ --no-check-certificate"


#Issue 6: scripts/git: git is too old: [1.9.1], building and installing: [2.1.4] to /usr/local/
	ERROR

	Solution: For the latest stable version for your release of Debian/Ubuntu
	For Ubuntu, this PPA provides the latest stable upstream Git version
	$ sudo add-apt-repository ppa:git-core/ppa
	$ sudo apt update
	$ sudo apt install git


#Issue 7: DTBS ERROR Building device tree overlays
	DTC     src/arm/BBAI_BB-BONE-FACE-8CH-00A0.dtbo ERROR
	
	Solution: Comment DT Overlays in line no 60 to 66 in "build-beagleboneblack.sh"


#Issue 8: U-boot ERROR /usr/include/libfdt_env.h:81:24: error: redefinition of ‘fdt16_to_cpu’ 
	
	Ref link: https://github.com/crust-firmware/meta/issues/2

	find -name 'libfdt*.h' -exec sed -i 's/ _LIBFDT_/ LIBFDT_/g' {} +
	find -name 'fdt.h' -exec sed -i 's/ _FDT_H/ FDT_H/g' {} +
