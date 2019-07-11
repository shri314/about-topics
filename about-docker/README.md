## Docker by examples:
- Presentation by Shriram
- 20th Nov 2017 (last updated)
		 
## Contents:

<!-- vim-markdown-toc GitLab -->

* [Docker glossary:](#docker-glossary:)
* [Building your own image:](#building-your-own-image:)
* [Creating a client application, and make it talk to the server application:](#creating-a-client-application,-and-make-it-talk-to-the-server-application:)
* [Working with docker compose - (using declarative syntax)](#working-with-docker-compose-(using-declarative-syntax))
* [Working with docker swarm, docker stack](#working-with-docker-swarm,-docker-stack)

<!-- vim-markdown-toc -->

1. `docker run hello-world`
		
        $ docker run hello-world
	    Unable to find image 'hello-world:latest' locally
	    latest: Pulling from library/hello-world
	    9a0669468bf7: Pull complete
	    Digest: sha256:cf2f6d004a59f7c18ec89df311cf0f6a1c714ec924eebcbfdd759a669b90e711
	    Status: Downloaded newer image for hello-world:latest
	    
	    Hello from Docker!
	    This message shows that your installation appears to be working correctly.
	    
	    To generate this message, Docker took the following steps:
	     1. The Docker client contacted the Docker daemon.
	     2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
	     3. The Docker daemon created a new container from that image which runs the
	    executable that produces the output you are currently reading.
	     4. The Docker daemon streamed that output to the Docker client, which sent it
	    to your terminal.
	    
	    To try something more ambitious, you can run an Ubuntu container with:
	     $ docker run -it ubuntu bash
	    
	    Share images, automate workflows, and more with a free Docker ID:
	     https://cloud.docker.com/
	    
	    For more examples and ideas, visit:
	     https://docs.docker.com/engine/userguide/

1. `docker images` | `docker image ls`

		$ docker images
		REPOSITORY            TAG                    IMAGE ID            CREATED             SIZE
		hello-world           latest                 725dcfab7d63        2 weeks ago         1.84kB

1. `docker run ubuntu:17.04`

        $ docker run ubuntu:17.04
		Unable to find image 'ubuntu:17.04' locally
		17.04: Pulling from library/ubuntu
		0bbeb3f34b71: Downloading [============>                                      ]  9.437MB/38.6MB
		fb8d5f4c517a: Download complete
		c4cd377f2172: Download complete
		968d05a75978: Download complete
		f358380db9ed: Download complete
		Digest: sha256:bac29fa4b3bfd3821784d0c69f272e57bd19327ba0dac8ad39151bb6cbbdd9f6
		Status: Downloaded newer image for ubuntu:17.04


1. `docker run ubuntu:17.04`

		$ docker run ubuntu:17.04
        $ 

1. `docker run ubuntu:17.04 bash`

		$ docker run ubuntu:17.04 bash
        $ 

1. `docker run -it ubuntu:17.04 bash`

		$ docker run -it ubuntu:17.04 bash
		root@9135d932a0fc:/# ls
		bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
		root@9135d932a0fc:/# exit
		exit

1. `docker run -it ubuntu:17.04 bash`

		$ docker run -it ubuntu:17.04 bash
		root@a766d02be5ee:/# ls
		bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
		root@a766d02be5ee:/# cd
		root@a766d02be5ee:~# ls
		root@a766d02be5ee:~#
		root@a766d02be5ee:~#
		root@a766d02be5ee:~# cd ~
		root@a766d02be5ee:~# pwd
		/root
		root@a766d02be5ee:~# echo abc > abc.txt
		root@a766d02be5ee:~# cat abc.txt
		abc
		root@a766d02be5ee:~# exit
		exit
		
		
		$ docker run -it ubuntu:17.04 bash
		root@b67cdae8c324:/# cd ~
		root@b67cdae8c324:~# pwd
		/root
		root@b67cdae8c324:~# ls
		root@b67cdae8c324:~# exit
		exit


1. `docker container ls` | `docker ps`

		$ docker container ls
		CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES


1. `docker container ls -a` | `docker ps -a`

		$ docker container ls -a
		CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
		b67cdae8c324        ubuntu:17.04        "bash"              3 minutes ago       Exited (0) 3 minutes ago                        condescending_goldwasser
		a766d02be5ee        ubuntu:17.04        "bash"              4 minutes ago       Exited (0) 3 minutes ago                        elastic_pasteur
		9135d932a0fc        ubuntu:17.04        "bash"              5 minutes ago       Exited (0) 5 minutes ago                        unruffled_torvalds
		f0c38799c22b        ubuntu:17.04        "/bin/bash"         7 minutes ago       Exited (0) 7 minutes ago                        clever_benz
		b24608850b1a        ubuntu:17.04        "/bin/bash"         7 minutes ago       Exited (0) 7 minutes ago                        practical_fermi
		2db206b423ca        hello-world         "/hello"            17 minutes ago      Exited (0) 17 minutes ago                       blissful_borg


1. `docker run -i -t -d ubuntu:17.04 top`

		$ docker run -i -t -d ubuntu:17.04 top
		ea115ac3344ef391634ad44839652478459b97cf5ba8a56c9681619949184ced
		
		
		$ docker ps
		CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS              PORTS               NAMES
		ea115ac3344e        ubuntu:17.04        "top"               About a minute ago   Up About a minute                       nervous_chandrasekhar
		
		
		$ docker attach ea115ac3344e
		top - 15:53:28 up 2 days,  3:36,  0 users,  load average: 0.00, 0.00, 0.00
		Tasks:   1 total,   1 running,   0 sleeping,   0 stopped,   0 zombie
		%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
		KiB Mem :  4037480 total,  2562304 free,   235240 used,  1239936 buff/cache
		KiB Swap:  7340028 total,  7340028 free,        0 used.  3508428 avail Mem
		
		  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
		    1 root      20   0   39016   3104   2648 R   0.0  0.1   0:00.06 top


## Docker glossary:

1. Images

	These are like tarballs containing everything needed for an application. They have a name and a tag. The smaller the image, faster it loads, and better. Images have layers.

1. Containers

	These are running instances of images. They are efermeral.

1. Docker Daemon

		$ ps -afe | grep docker
		root      6167     1  1 Nov17 ?        00:41:40 /usr/bin/dockerd -H fd://
		root      6406  6167  0 Nov17 ?        00:04:05 docker-containerd -l unix:///var/run/docker/libcontainerd/docker-containerd.sock --metrics-interval=0 --start-timeout 2m --state-dir /var/run/docker/libcontainerd/containerd --shim docker-containerd-shim --runtime docker-runc

1. Docker Client

		$ which docker
		/usr/bin/docker
		
		$ docker --version
		Docker version 17.09.0-ce, build afdb6d4
		
		$ sudo ls -l -F /var/run/docker/libcontainerd/docker-containerd.sock
		srw-rw---- 1 root root 0 Nov 17 17:48 /var/run/docker/libcontainerd/docker-containerd.sock=


## Building your own image:

1. `Dockerfile` and `docker build`

		$ ls
		ABC.sh*  Dockerfile

		$ cat Dockerfile
		FROM ubuntu:17.04
		RUN apt-get update
		RUN apt-get install psmisc
		COPY ABC.sh /root/ABC.sh
		RUN chmod +x ~/ABC.sh
		CMD /root/ABC.sh
        
        $ cat ABC.sh
		#!/bin/bash
		
		while [ true ]
		do
		   pstree -aAp
		   date
		   sleep 2
		done

		$ docker build .
		Sending build context to Docker daemon  3.072kB
		Step 1/6 : FROM ubuntu:17.04
		 ---> 93fd6b1bc1dc
		Step 2/6 : RUN apt-get update -y
		 ---> Running in 208ae3dfd0df
		Get:1 http://security.ubuntu.com/ubuntu zesty-security InRelease [89.2 kB]
		Get:2 http://archive.ubuntu.com/ubuntu zesty InRelease [243 kB]
		Get:3 http://security.ubuntu.com/ubuntu zesty-security/universe Sources [31.9 kB]
		Get:4 http://archive.ubuntu.com/ubuntu zesty-updates InRelease [89.2 kB]
		Get:5 http://archive.ubuntu.com/ubuntu zesty-backports InRelease [89.2 kB]
		Get:6 http://security.ubuntu.com/ubuntu zesty-security/universe amd64 Packages [103 kB]
		Get:7 http://archive.ubuntu.com/ubuntu zesty/universe Sources [10.7 MB]
		Get:8 http://security.ubuntu.com/ubuntu zesty-security/multiverse amd64 Packages [3104 B]
		Get:9 http://security.ubuntu.com/ubuntu zesty-security/main amd64 Packages [202 kB]
		Get:10 http://security.ubuntu.com/ubuntu zesty-security/restricted amd64 Packages [3221 B]
		Get:11 http://archive.ubuntu.com/ubuntu zesty/restricted amd64 Packages [14.3 kB]
		Get:12 http://archive.ubuntu.com/ubuntu zesty/main amd64 Packages [1574 kB]
		Get:13 http://archive.ubuntu.com/ubuntu zesty/multiverse amd64 Packages [189 kB]
		Get:14 http://archive.ubuntu.com/ubuntu zesty/universe amd64 Packages [10.5 MB]
		Get:15 http://archive.ubuntu.com/ubuntu zesty-updates/universe Sources [78.2 kB]
		Get:16 http://archive.ubuntu.com/ubuntu zesty-updates/universe amd64 Packages [206 kB]
		Get:17 http://archive.ubuntu.com/ubuntu zesty-updates/restricted amd64 Packages [3604 B]
		Get:18 http://archive.ubuntu.com/ubuntu zesty-updates/multiverse amd64 Packages [13.2 kB]
		Get:19 http://archive.ubuntu.com/ubuntu zesty-updates/main amd64 Packages [305 kB]
		Get:20 http://archive.ubuntu.com/ubuntu zesty-backports/main amd64 Packages [1698 B]
		Get:21 http://archive.ubuntu.com/ubuntu zesty-backports/universe amd64 Packages [3226 B]
		Fetched 24.5 MB in 46s (522 kB/s)
		Reading package lists...
		 ---> ce41f82e3bb0
		Removing intermediate container 208ae3dfd0df
		Step 3/6 : RUN apt-get install -y psmisc
		 ---> Running in 9153aca118ed
		Reading package lists...
		Building dependency tree...
		Reading state information...
		The following NEW packages will be installed:
		  psmisc
		0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
		Need to get 48.0 kB of archives.
		After this operation, 238 kB of additional disk space will be used.
		Get:1 http://archive.ubuntu.com/ubuntu zesty/main amd64 psmisc amd64 22.21-2.1build1 [48.0 kB]
		debconf: delaying package configuration, since apt-utils is not installed
		Fetched 48.0 kB in 0s (99.5 kB/s)
		Selecting previously unselected package psmisc.
		(Reading database ... 4078 files and directories currently installed.)
		Preparing to unpack .../psmisc_22.21-2.1build1_amd64.deb ...
		Unpacking psmisc (22.21-2.1build1) ...
		Setting up psmisc (22.21-2.1build1) ...
		 ---> 1161111326e8
		Removing intermediate container 9153aca118ed
		Step 4/6 : COPY ABC.sh /root/ABC.sh
		 ---> 9bc1bd9a2670
		Step 5/6 : RUN chmod +x ~/ABC.sh
		 ---> Running in 16ae27f3f394
		 ---> 8d84df206745
		Removing intermediate container 16ae27f3f394
		Step 6/6 : CMD /root/ABC.sh
		 ---> Running in df93e9473536
		 ---> fb414f4cf100
		Removing intermediate container df93e9473536
		Successfully built fb414f4cf100

		$ docker images
		REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
		<none>              <none>              fb414f4cf100        About a minute ago   135MB
		ubuntu              17.04               93fd6b1bc1dc        44 hours ago         95.4MB

		$ docker build -t shri314/abcd:myapp .
		Sending build context to Docker daemon  3.072kB
		Step 1/6 : FROM ubuntu:17.04
		 ---> 93fd6b1bc1dc
		Step 2/6 : RUN apt-get update -y
		 ---> Using cache
		 ---> ce41f82e3bb0
		Step 3/6 : RUN apt-get install -y psmisc
		 ---> Using cache
		 ---> 1161111326e8
		Step 4/6 : COPY ABC.sh /root/ABC.sh
		 ---> Using cache
		 ---> 9bc1bd9a2670
		Step 5/6 : RUN chmod +x ~/ABC.sh
		 ---> Using cache
		 ---> 8d84df206745
		Step 6/6 : CMD /root/ABC.sh
		 ---> Using cache
		 ---> fb414f4cf100
		Successfully built fb414f4cf100
		Successfully tagged shri314/abcd:myapp


		$ docker images
		REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
		shri314/myapp       mytag               fb414f4cf100        About a minute ago   135MB
		ubuntu              17.04               93fd6b1bc1dc        44 hours ago         95.4MB

		$ docker run -it shri314/abcd:mytag
		sh -c /root/ABC.sh
		  `-ABC.sh /root/ABC.sh
		      `-pstree -aA
		Sun Nov 19 17:34:07 UTC 2017
        ^C

1. Lets build a service in python

		$ docker build -t shri314/server-app .
		Sending build context to Docker daemon  3.072kB
		Step 1/7 : FROM ubuntu:latest
		 ---> 20c44cd7596f
		Step 2/7 : RUN apt-get update -y
		 ---> Using cache
		 ---> cb482ad7ec10
		Step 3/7 : RUN apt-get install -y python-flask python-flask-api
		 ---> Running in 2ba1240f8920
		Reading package lists...
		Building dependency tree...
		Reading state information...
		The following additional packages will be installed:
		  file javascript-common libexpat1 libffi6 libjs-bootstrap libjs-jquery
		  libjs-prettify libmagic1 libpython-stdlib libpython2.7-minimal
		  libpython2.7-stdlib libsqlite3-0 libssl1.0.0 mime-support python
		  python-blinker python-cffi-backend python-cryptography python-enum34
		  python-flask-api-common python-idna python-ipaddress python-itsdangerous
		  python-jinja2 python-markupsafe python-minimal python-openssl
		  python-pkg-resources python-pyasn1 python-pyinotify python-six
		  python-werkzeug python2.7 python2.7-minimal
		Suggested packages:
		  apache2 | lighttpd | httpd python-doc python-tk python-blinker-doc
		  python-cryptography-doc python-cryptography-vectors python-enum34-doc
		  python-flask-doc python-jinja2-doc python-openssl-doc python-openssl-dbg
		  python-setuptools doc-base python-pyinotify-doc ipython python-genshi
		  python-lxml python-greenlet python-redis python-pylibmc | python-memcache
		  python-werkzeug-doc python2.7-doc binutils binfmt-support
		The following NEW packages will be installed:
		  file javascript-common libexpat1 libffi6 libjs-bootstrap libjs-jquery
		  libjs-prettify libmagic1 libpython-stdlib libpython2.7-minimal
		  libpython2.7-stdlib libsqlite3-0 libssl1.0.0 mime-support python
		  python-blinker python-cffi-backend python-cryptography python-enum34
		  python-flask python-flask-api python-flask-api-common python-idna
		  python-ipaddress python-itsdangerous python-jinja2 python-markupsafe
		  python-minimal python-openssl python-pkg-resources python-pyasn1
		  python-pyinotify python-six python-werkzeug python2.7 python2.7-minimal
		0 upgraded, 36 newly installed, 0 to remove and 0 not upgraded.
		Need to get 7210 kB of archives.
		After this operation, 33.7 MB of additional disk space will be used.
		Get:1 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libpython2.7-minimal amd64 2.7.12-1ubuntu0~16.04.1 [339 kB]
		Get:2 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 python2.7-minimal amd64 2.7.12-1ubuntu0~16.04.1 [1295 kB]
		Get:3 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-minimal amd64 2.7.11-1 [28.2 kB]
		Get:4 http://archive.ubuntu.com/ubuntu xenial/main amd64 mime-support all 3.59ubuntu1 [31.0 kB]
		Get:5 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libexpat1 amd64 2.1.0-7ubuntu0.16.04.3 [71.2 kB]
		Get:6 http://archive.ubuntu.com/ubuntu xenial/main amd64 libffi6 amd64 3.2.1-4 [17.8 kB]
		Get:7 http://archive.ubuntu.com/ubuntu xenial/main amd64 libsqlite3-0 amd64 3.11.0-1ubuntu1 [396 kB]
		Get:8 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libssl1.0.0 amd64 1.0.2g-1ubuntu4.9 [1085 kB]
		Get:9 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libpython2.7-stdlib amd64 2.7.12-1ubuntu0~16.04.1 [1884 kB]
		Get:10 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 python2.7 amd64 2.7.12-1ubuntu0~16.04.1 [224 kB]
		Get:11 http://archive.ubuntu.com/ubuntu xenial/main amd64 libpython-stdlib amd64 2.7.11-1 [7656 B]
		Get:12 http://archive.ubuntu.com/ubuntu xenial/main amd64 python amd64 2.7.11-1 [137 kB]
		Get:13 http://archive.ubuntu.com/ubuntu xenial/main amd64 libmagic1 amd64 1:5.25-2ubuntu1 [216 kB]
		Get:14 http://archive.ubuntu.com/ubuntu xenial/main amd64 file amd64 1:5.25-2ubuntu1 [21.2 kB]
		Get:15 http://archive.ubuntu.com/ubuntu xenial/main amd64 javascript-common all 11 [6066 B]
		Get:16 http://archive.ubuntu.com/ubuntu xenial/universe amd64 libjs-bootstrap all 3.3.6+dfsg-1 [227 kB]
		Get:17 http://archive.ubuntu.com/ubuntu xenial/main amd64 libjs-jquery all 1.11.3+dfsg-4 [161 kB]
		Get:18 http://archive.ubuntu.com/ubuntu xenial/universe amd64 libjs-prettify all 2013.03.04+dfsg-4 [36.6 kB]
		Get:19 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-blinker all 1.3.dfsg2-1build1 [12.4 kB]
		Get:20 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-cffi-backend amd64 1.5.2-1ubuntu1 [58.1 kB]
		Get:21 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-enum34 all 1.1.2-1 [35.8 kB]
		Get:22 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-idna all 2.0-3 [35.1 kB]
		Get:23 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-ipaddress all 1.0.16-1 [18.0 kB]
		Get:24 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-pkg-resources all 20.7.0-1 [108 kB]
		Get:25 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-pyasn1 all 0.1.9-1 [45.1 kB]
		Get:26 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-six all 1.10.0-3 [10.9 kB]
		Get:27 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 python-cryptography amd64 1.2.3-1ubuntu0.1 [199 kB]
		Get:28 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-itsdangerous all 0.24+dfsg1-1 [12.0 kB]
		Get:29 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-markupsafe amd64 0.23-2build2 [15.5 kB]
		Get:30 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-jinja2 all 2.8-1 [109 kB]
		Get:31 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 python-werkzeug all 0.10.4+dfsg1-1ubuntu1.1 [162 kB]
		Get:32 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-flask all 0.10.1-2build2 [51.8 kB]
		Get:33 http://archive.ubuntu.com/ubuntu xenial/universe amd64 python-flask-api-common all 0.6.4+dfsg-1 [28.3 kB]
		Get:34 http://archive.ubuntu.com/ubuntu xenial/universe amd64 python-flask-api all 0.6.4+dfsg-1 [16.1 kB]
		Get:35 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-openssl all 0.15.1-2build1 [84.1 kB]
		Get:36 http://archive.ubuntu.com/ubuntu xenial/main amd64 python-pyinotify all 0.9.6-0fakesync1 [24.6 kB]
		debconf: delaying package configuration, since apt-utils is not installed
		Fetched 7210 kB in 14s (493 kB/s)
		Selecting previously unselected package libpython2.7-minimal:amd64.
		(Reading database ... 4768 files and directories currently installed.)
		Preparing to unpack .../libpython2.7-minimal_2.7.12-1ubuntu0~16.04.1_amd64.deb ...
		Unpacking libpython2.7-minimal:amd64 (2.7.12-1ubuntu0~16.04.1) ...
		Selecting previously unselected package python2.7-minimal.
		Preparing to unpack .../python2.7-minimal_2.7.12-1ubuntu0~16.04.1_amd64.deb ...
		Unpacking python2.7-minimal (2.7.12-1ubuntu0~16.04.1) ...
		Selecting previously unselected package python-minimal.
		Preparing to unpack .../python-minimal_2.7.11-1_amd64.deb ...
		Unpacking python-minimal (2.7.11-1) ...
		Selecting previously unselected package mime-support.
		Preparing to unpack .../mime-support_3.59ubuntu1_all.deb ...
		Unpacking mime-support (3.59ubuntu1) ...
		Selecting previously unselected package libexpat1:amd64.
		Preparing to unpack .../libexpat1_2.1.0-7ubuntu0.16.04.3_amd64.deb ...
		Unpacking libexpat1:amd64 (2.1.0-7ubuntu0.16.04.3) ...
		Selecting previously unselected package libffi6:amd64.
		Preparing to unpack .../libffi6_3.2.1-4_amd64.deb ...
		Unpacking libffi6:amd64 (3.2.1-4) ...
		Selecting previously unselected package libsqlite3-0:amd64.
		Preparing to unpack .../libsqlite3-0_3.11.0-1ubuntu1_amd64.deb ...
		Unpacking libsqlite3-0:amd64 (3.11.0-1ubuntu1) ...
		Selecting previously unselected package libssl1.0.0:amd64.
		Preparing to unpack .../libssl1.0.0_1.0.2g-1ubuntu4.9_amd64.deb ...
		Unpacking libssl1.0.0:amd64 (1.0.2g-1ubuntu4.9) ...
		Selecting previously unselected package libpython2.7-stdlib:amd64.
		Preparing to unpack .../libpython2.7-stdlib_2.7.12-1ubuntu0~16.04.1_amd64.deb ...
		Unpacking libpython2.7-stdlib:amd64 (2.7.12-1ubuntu0~16.04.1) ...
		Selecting previously unselected package python2.7.
		Preparing to unpack .../python2.7_2.7.12-1ubuntu0~16.04.1_amd64.deb ...
		Unpacking python2.7 (2.7.12-1ubuntu0~16.04.1) ...
		Selecting previously unselected package libpython-stdlib:amd64.
		Preparing to unpack .../libpython-stdlib_2.7.11-1_amd64.deb ...
		Unpacking libpython-stdlib:amd64 (2.7.11-1) ...
		Processing triggers for libc-bin (2.23-0ubuntu9) ...
		Setting up libpython2.7-minimal:amd64 (2.7.12-1ubuntu0~16.04.1) ...
		Setting up python2.7-minimal (2.7.12-1ubuntu0~16.04.1) ...
		Linking and byte-compiling packages for runtime python2.7...
		Setting up python-minimal (2.7.11-1) ...
		Selecting previously unselected package python.
		(Reading database ... 5579 files and directories currently installed.)
		Preparing to unpack .../python_2.7.11-1_amd64.deb ...
		Unpacking python (2.7.11-1) ...
		Selecting previously unselected package libmagic1:amd64.
		Preparing to unpack .../libmagic1_1%3a5.25-2ubuntu1_amd64.deb ...
		Unpacking libmagic1:amd64 (1:5.25-2ubuntu1) ...
		Selecting previously unselected package file.
		Preparing to unpack .../file_1%3a5.25-2ubuntu1_amd64.deb ...
		Unpacking file (1:5.25-2ubuntu1) ...
		Selecting previously unselected package javascript-common.
		Preparing to unpack .../javascript-common_11_all.deb ...
		Unpacking javascript-common (11) ...
		Selecting previously unselected package libjs-bootstrap.
		Preparing to unpack .../libjs-bootstrap_3.3.6+dfsg-1_all.deb ...
		Unpacking libjs-bootstrap (3.3.6+dfsg-1) ...
		Selecting previously unselected package libjs-jquery.
		Preparing to unpack .../libjs-jquery_1.11.3+dfsg-4_all.deb ...
		Unpacking libjs-jquery (1.11.3+dfsg-4) ...
		Selecting previously unselected package libjs-prettify.
		Preparing to unpack .../libjs-prettify_2013.03.04+dfsg-4_all.deb ...
		Unpacking libjs-prettify (2013.03.04+dfsg-4) ...
		Selecting previously unselected package python-blinker.
		Preparing to unpack .../python-blinker_1.3.dfsg2-1build1_all.deb ...
		Unpacking python-blinker (1.3.dfsg2-1build1) ...
		Selecting previously unselected package python-cffi-backend.
		Preparing to unpack .../python-cffi-backend_1.5.2-1ubuntu1_amd64.deb ...
		Unpacking python-cffi-backend (1.5.2-1ubuntu1) ...
		Selecting previously unselected package python-enum34.
		Preparing to unpack .../python-enum34_1.1.2-1_all.deb ...
		Unpacking python-enum34 (1.1.2-1) ...
		Selecting previously unselected package python-idna.
		Preparing to unpack .../python-idna_2.0-3_all.deb ...
		Unpacking python-idna (2.0-3) ...
		Selecting previously unselected package python-ipaddress.
		Preparing to unpack .../python-ipaddress_1.0.16-1_all.deb ...
		Unpacking python-ipaddress (1.0.16-1) ...
		Selecting previously unselected package python-pkg-resources.
		Preparing to unpack .../python-pkg-resources_20.7.0-1_all.deb ...
		Unpacking python-pkg-resources (20.7.0-1) ...
		Selecting previously unselected package python-pyasn1.
		Preparing to unpack .../python-pyasn1_0.1.9-1_all.deb ...
		Unpacking python-pyasn1 (0.1.9-1) ...
		Selecting previously unselected package python-six.
		Preparing to unpack .../python-six_1.10.0-3_all.deb ...
		Unpacking python-six (1.10.0-3) ...
		Selecting previously unselected package python-cryptography.
		Preparing to unpack .../python-cryptography_1.2.3-1ubuntu0.1_amd64.deb ...
		Unpacking python-cryptography (1.2.3-1ubuntu0.1) ...
		Selecting previously unselected package python-itsdangerous.
		Preparing to unpack .../python-itsdangerous_0.24+dfsg1-1_all.deb ...
		Unpacking python-itsdangerous (0.24+dfsg1-1) ...
		Selecting previously unselected package python-markupsafe.
		Preparing to unpack .../python-markupsafe_0.23-2build2_amd64.deb ...
		Unpacking python-markupsafe (0.23-2build2) ...
		Selecting previously unselected package python-jinja2.
		Preparing to unpack .../python-jinja2_2.8-1_all.deb ...
		Unpacking python-jinja2 (2.8-1) ...
		Selecting previously unselected package python-werkzeug.
		Preparing to unpack .../python-werkzeug_0.10.4+dfsg1-1ubuntu1.1_all.deb ...
		Unpacking python-werkzeug (0.10.4+dfsg1-1ubuntu1.1) ...
		Selecting previously unselected package python-flask.
		Preparing to unpack .../python-flask_0.10.1-2build2_all.deb ...
		Unpacking python-flask (0.10.1-2build2) ...
		Selecting previously unselected package python-flask-api-common.
		Preparing to unpack .../python-flask-api-common_0.6.4+dfsg-1_all.deb ...
		Unpacking python-flask-api-common (0.6.4+dfsg-1) ...
		Selecting previously unselected package python-flask-api.
		Preparing to unpack .../python-flask-api_0.6.4+dfsg-1_all.deb ...
		Unpacking python-flask-api (0.6.4+dfsg-1) ...
		Selecting previously unselected package python-openssl.
		Preparing to unpack .../python-openssl_0.15.1-2build1_all.deb ...
		Unpacking python-openssl (0.15.1-2build1) ...
		Selecting previously unselected package python-pyinotify.
		Preparing to unpack .../python-pyinotify_0.9.6-0fakesync1_all.deb ...
		Unpacking python-pyinotify (0.9.6-0fakesync1) ...
		Processing triggers for libc-bin (2.23-0ubuntu9) ...
		Setting up mime-support (3.59ubuntu1) ...
		Setting up libexpat1:amd64 (2.1.0-7ubuntu0.16.04.3) ...
		Setting up libffi6:amd64 (3.2.1-4) ...
		Setting up libsqlite3-0:amd64 (3.11.0-1ubuntu1) ...
		Setting up libssl1.0.0:amd64 (1.0.2g-1ubuntu4.9) ...
		debconf: unable to initialize frontend: Dialog
		debconf: (TERM is not set, so the dialog frontend is not usable.)
		debconf: falling back to frontend: Readline
		debconf: unable to initialize frontend: Readline
		debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.22.1 /usr/local/share/perl/5.22.1 /usr/lib/x86_64-linux-gnu/perl5/5.22 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl/5.22 /usr/share/perl/5.22 /usr/local/lib/site_perl /usr/lib/x86_64-linux-gnu/perl-base .) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)
		debconf: falling back to frontend: Teletype
		Setting up libpython2.7-stdlib:amd64 (2.7.12-1ubuntu0~16.04.1) ...
		Setting up python2.7 (2.7.12-1ubuntu0~16.04.1) ...
		Setting up libpython-stdlib:amd64 (2.7.11-1) ...
		Setting up python (2.7.11-1) ...
		Setting up libmagic1:amd64 (1:5.25-2ubuntu1) ...
		Setting up file (1:5.25-2ubuntu1) ...
		Setting up javascript-common (11) ...
		Setting up libjs-bootstrap (3.3.6+dfsg-1) ...
		Setting up libjs-jquery (1.11.3+dfsg-4) ...
		Setting up libjs-prettify (2013.03.04+dfsg-4) ...
		Setting up python-blinker (1.3.dfsg2-1build1) ...
		Setting up python-cffi-backend (1.5.2-1ubuntu1) ...
		Setting up python-enum34 (1.1.2-1) ...
		Setting up python-idna (2.0-3) ...
		Setting up python-ipaddress (1.0.16-1) ...
		Setting up python-pkg-resources (20.7.0-1) ...
		Setting up python-pyasn1 (0.1.9-1) ...
		Setting up python-six (1.10.0-3) ...
		Setting up python-cryptography (1.2.3-1ubuntu0.1) ...
		Setting up python-itsdangerous (0.24+dfsg1-1) ...
		Setting up python-markupsafe (0.23-2build2) ...
		Setting up python-jinja2 (2.8-1) ...
		Setting up python-werkzeug (0.10.4+dfsg1-1ubuntu1.1) ...
		Setting up python-flask (0.10.1-2build2) ...
		Setting up python-flask-api-common (0.6.4+dfsg-1) ...
		Setting up python-flask-api (0.6.4+dfsg-1) ...
		Setting up python-openssl (0.15.1-2build1) ...
		Setting up python-pyinotify (0.9.6-0fakesync1) ...
		Processing triggers for libc-bin (2.23-0ubuntu9) ...
		 ---> 0c377d8b8077
		Removing intermediate container 2ba1240f8920
		Step 4/7 : COPY . /app
		 ---> 765aa034169e
		Step 5/7 : WORKDIR /app
		 ---> a500599f94ff
		Removing intermediate container 0bf19cfdb34a
		Step 6/7 : ENTRYPOINT python
		 ---> Running in 8eca9cc5ab45
		 ---> efc51898a1ad
		Removing intermediate container 8eca9cc5ab45
		Step 7/7 : CMD app.py
		 ---> Running in a79751d8e3c7
		 ---> 85ee9eddf6d2
		Removing intermediate container a79751d8e3c7
		Successfully built 85ee9eddf6d2
		Successfully tagged shri314/server-app:latest


		$ docker run -it --entrypoint bash shri314/server-app
        root@84f1c1d67dd2:/app# python app.py
		 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
		^C
		root@84f1c1d67dd2:/app# exit
		exit

		$ docker run -d shri314/server-app
		aa176c19c411a443a72a7bece95682c24a1fe07fa90a8d63d22a02125e1d6d0c
          
        $ docker ps
		CONTAINER ID        IMAGE                  COMMAND             CREATED             STATUS              PORTS               NAMES
		aa176c19c411        shri314/server-app     "python app.py"     32 seconds ago      Up 31 seconds                           sad_gates

        $ sudo netstat -anp | grep 5000 -w | grep LISTEN

        $ docker exec -it aa176c19c411 bash
		root@0d1eddcb70c9:/app# 
		root@0d1eddcb70c9:/app# netstat -anp | grep 5000 -w | grep LISTE
		tcp        0      0 0.0.0.0:5000            0.0.0.0:*               LISTEN      1/python
		root@0d1eddcb70c9:/app# exit
		exit

        $ docker container inspect 14e6bce8e6a9 | grep IPAddress -w
            "IPAddress": "172.17.0.2",
                    "IPAddress": "172.17.0.2",

        $ telnet 172.17.0.2 5000
		Trying 172.17.0.2...
		Connected to 172.17.0.2.
		Escape character is '^]'.
		GET /nads HTTP/1.1
		
		HTTP/1.0 200 OK
		Content-Type: text/html; charset=utf-8
		Content-Length: 20
		Server: Werkzeug/0.10.4 Python/2.7.12
		Date: Sun, 19 Nov 2017 18:34:22 GMT
		
		Hello World - nads!
		Connection closed by foreign host.


		$ docker run -p 8888:5000 -d shri314/server-app
		0fde9e83d8a029d21e476c8d6c08d477e3666d7f5ce3c70b419312baf6bf1145

		$ telnet 127.0.0.1 8888
		Trying 127.0.0.1...
		Connected to 127.0.0.1.
		Escape character is '^]'.
		GET /dsjds HTTP/1.1
		
		HTTP/1.0 200 OK
		Content-Type: text/html; charset=utf-8
		Content-Length: 21
		Server: Werkzeug/0.10.4 Python/2.7.12
		Date: Sun, 19 Nov 2017 18:37:44 GMT
		
		Hello World - dsjds!
		Connection closed by foreign host.

		$ sudo netstat -anp | grep 8888 -w | grep LISTEN
		tcp6       0      0 :::8888                 :::*                    LISTEN      29920/docker-proxy


## Creating a client application, and make it talk to the server application:

1. Lets build a client application that uses the python service

        $ cat Dockerfile
        FROM ubuntu:17.04
        RUN apt-get update -y
        RUN apt-get install -y telnet curl
        COPY ABC.sh /root/ABC.sh
        RUN chmod +x ~/ABC.sh
        CMD /root/ABC.sh

        $ cat ABC.sh
        #!/bin/bash
        
        while [ true ]
        do
           curl server-app:5000/abc-${RANDOM}-def
           date
           sleep 2
        done

        $ docker build -t shri314/client-app .
        
        $ docker run -it --entrypoint bash shri314/client-app
        root@2b71ea40722a:/# telnet 172.17.0.2 5000
        Trying 172.17.0.2...
        Connected to 172.17.0.2.
        Escape character is '^]'.
        GET /aaaaaa
        
        Hello World - aaaaaa!
        Connection closed by foreign host.
        root@2b71ea40722a:/# exit
        exit
        
        $ docker network create mynet
        9a9bc54c758177c803d61902b1c2bcb5c77297f9267c8f288119ebf7cadb3fdb
        
        $ docker network ls
        NETWORK ID          NAME                DRIVER              SCOPE
        72ee593e6676        bridge              bridge              local
        89f52701d1b5        docker_gwbridge     bridge              local
        c4596d337dcd        host                host                local
        9a9bc54c7581        mynet               bridge              local
        fca815a1d12c        none                null                local
        
        $ docker run -d --net mynet --name server-app shri314/server-app
        43de136955576d3332977599ddb4c8e1bdb09b492480cabd4b253f865a62265b
        
        $ docker ps
        CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS              PORTS               NAMES
        43de13695557        shri314/server-app    "python app.py"     5 seconds ago       Up 4 seconds                            server-app
        
        $ docker run -it --net mynet --entrypoint bash shri314/client-app
        root@782aa9155a8d:/# ping server-app
        PING server-app (172.18.0.2) 56(84) bytes of data.
        64 bytes from server-app.mynet (172.18.0.2): icmp_seq=1 ttl=64 time=0.056 ms
        64 bytes from server-app.mynet (172.18.0.2): icmp_seq=2 ttl=64 time=0.055 ms
        64 bytes from server-app.mynet (172.18.0.2): icmp_seq=3 ttl=64 time=0.056 ms
        ^C
        root@782aa9155a8d:/# curl 'server-app:5000/abc'
        Hello World - abc!
        root@782aa9155a8d:/# exit
        exit
        
        $ docker run -it --net mynet shri314/client-app
        Hello World - abc-613-def!
        Sun Nov 19 20:01:29 UTC 2017
        Hello World - abc-22533-def!
        Sun Nov 19 20:01:31 UTC 2017
        Hello World - abc-18672-def!
        Sun Nov 19 20:01:33 UTC 2017
        Hello World - abc-12524-def!
        Sun Nov 19 20:01:35 UTC 2017
        Hello World - abc-1325-def!
        Sun Nov 19 20:01:37 UTC 2017
        Hello World - abc-1733-def!
        Sun Nov 19 20:01:39 UTC 2017
        ^C


## Working with docker compose - (using declarative syntax)

1. Deploying images on current machine using: `docker-compose`

        $ pwd
        /home/shriram/dd
        
        $ ls
        docker-compose.yml
        
        $ cat docker-compose.yml
        version: "3.3"
        
        services:
           server-app:
              image: 'shri314/server-app'
        
           client-app:
              image: 'shri314/client-app'
        
        $ docker-compose up
        docker-compose up
        Creating network "dd_default" with the default driver
        Creating dd_server-app_1 ...
        Creating dd_client-app_1 ...
        Creating dd_client-app_1
        Creating dd_client-app_1 ... done
        Attaching to dd_server-app_1, dd_client-app_1
        server-app_1  |  * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
        server-app_1  | 172.18.0.2 - - [20/Nov/2017 10:47:36] "GET /abc-27342-def HTTP/1.1" 200 -
        client-app_1  |   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
        client-app_1  |                                  Dload  Upload   Total   Spent    Left  Speed
          0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:-100    29  100    29    0     0   3859      0 --:--:-- --:--:--
        --:--:--  4142
        client-app_1  | Hello World - abc-27342-def!
        client-app_1  | Mon Nov 20 10:47:36 UTC 2017
        client-app_1  |   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
        client-app_1  |                                  Dload  Upload   Total   Spent    Left  Speed
        server-app_1  | 172.18.0.2 - - [20/Nov/2017 10:47:38] "GET /abc-9504-def HTTP/1.1" 200 -
          0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:-100    28  100    28    0     0   4620      0 --:--:-- --:--:--
        --:--:--  5600
        ^C
        Gracefully stopping... (press Ctrl+C again to force)
        Stopping dd_server-app_1 ...
        Stopping dd_client-app_1 ...
        Killing dd_server-app_1 ... done
        Killing dd_client-app_1 ... done
        
        $ docker-compose down
        Removing service abc_client-app
        Removing service abc_server-app
        Removing network abc_default
        
        $ docker-compose up -d
        Starting dd_server-app_1 ...
        Starting dd_server-app_1
        Starting dd_client-app_1 ...
        Starting dd_client-app_1 ... done

1. Checking/Extracting logs `docker-compose logs -f`

        $ pwd
        /home/shriram/dd
        
        $ docker-compose logs -f
        Attaching to dd_server-app_1, dd_client-app_1
        server-app_1  |  * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
        server-app_1  | 172.18.0.2 - - [20/Nov/2017 10:47:36] "GET /abc-27342-def HTTP/1.1" 200 -
        server-app_1  | 172.18.0.2 - - [20/Nov/2017 10:47:54] "GET /abc-31898-def HTTP/1.1" 200 -
        client-app_1  |   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
        server-app_1  | 172.18.0.2 - - [20/Nov/2017 10:48:10] "GET /abc-24427-def HTTP/1.1" 200 -
        client-app_1  |                                  Dload  Upload   Total   Spent    Left  Speed
        server-app_1  | 172.18.0.2 - - [20/Nov/2017 10:48:12] "GET /abc-8244-def HTTP/1.1" 200 -
          0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:-100    29  100    29    0     0   3859      0 --:--:-
        --:--:--  4142
        client-app_1  | Hello World - abc-16614-def!
        client-app_1  | Mon Nov 20 10:47:44 UTC 2017
        client-app_1  |   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
        client-app_1  |                                  Dload  Upload   Total   Spent    Left  Speed
          0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:-100    29  100    29    0     0   4696      0 --:--:-
        --:--:--  5800
        client-app_1  | Hello World - abc-15749-def!
        server-app_1  |  * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
        client-app_1  | Mon Nov 20 10:47:46 UTC 2
        server-app_1  | 172.18.0.3 - - [20/Nov/2017 10:48:31] "GET /abc-26941-def HTTP/1.1" 200 -
        client-app_1  |   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
        server-app_1  | 172.18.0.3 - - [20/Nov/2017 10:48:51] "GET /abc-19153-def HTTP/1.1" 200 -
        server-app_1  | 172.18.0.3 - - [20/Nov/2017 10:48:53] "GET /abc-27683-def HTTP/1.1" 200 -
        client-app_1  |                                  Dload  Upload   Total   Spent    Left  Speed
        client-app_1  | Hello World - abc-701-def!
          0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:-100    27  100    27    0     0   4478      0 --:--:-
        --:--:--  5400
        client-app_1  | Hello World - abc-19126-def!
        client-app_1  | Mon Nov 20 10:48:59 UTC 2017
        ^C
        ERROR: Aborting.


1. Building with `docker-compose build`

        $ ls
        client/  docker-compose.yml  server/
        
        $ cat docker-compose.yml
        version: "3.3"
        
        services:
           server-app:
              image: 'shri314/server-app'
              build:
                 context: server
                 dockerfile: 'Dockerfile'
        
           client-app:
              image: 'shri314/client-app'
              build:
                 context: client
                 dockerfile: 'Dockerfile'
        
        $ ls client
        ABC.sh*  Dockerfile
        
        $ ls server
        Dockerfile  app.py
        
        $ docker-compose build

1. docker-compose push

## Working with docker swarm, docker stack

Docker's native clustering solution

1. docker swarm init

        $ docker swarm init
        Swarm initialized: current node (vslhdun2ot6x5egj9pp8xgg6w) is now a manager.
        
        To add a worker to this swarm, run the following command:
        
            docker swarm join --token SWMTKN-1-4d6qvqydafvfvwgz9ysmzkmq9a2k2xjz      s1gpc2oqesiu7mpuxn-8tkgpnilb9de58eubhnj0rk44 192.168.128.12:2377
        
        To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.


1. Deploying across swarm nodes with `docker stack deploy --compose-file docker-compose.yml abc`

        $ ls
        client/  docker-compose.yml  server/
        
        $ hostname
        charm-u16
        
        $ docker stack deploy --compose-file docker-compose.yml abc
        Ignoring unsupported options: build
        
        Creating network abc_default
        Creating service abc_server-app
        Creating service abc_client-app
        
        $ docker stack ls
        NAME                SERVICES
        abc                 2
        
        $ docker stack ps abc
        ID                  NAME                IMAGE                       NODE                DESIRED STATE       CURRENT STATE               ERROR               PORTS
        c6avpy4dk4wq        abc_client-app.1    shri314/client-app:latest   charm-u16           Running             Running about an hour ago    
        i3ahumblkgpb        abc_server-app.1    shri314/server-app:latest   charm-u16           Running             Running about an hour ago

        $ docker stack services abc
        ID                  NAME                MODE                REPLICAS            IMAGE                     PORTS
        txb9qup1yn3m        abc_server-app      replicated          1/1                 shri314/server-app:latest
        wivmso24yeho        abc_client-app      replicated          1/1                 shri314/client-app:latest

        $ docker service logs --tail 5  txb9qup1yn3m
        abc_server-app.1.i3ahumblkgpb@charm-u16    | 10.0.0.5 - - [20/Nov/2017 12:56:36] "GET /abc-15185-def HTTP/1.1" 200 -
        abc_server-app.1.i3ahumblkgpb@charm-u16    | 10.0.0.5 - - [20/Nov/2017 12:56:36] "GET /abc-5806-def HTTP/1.1" 200 -
        abc_server-app.1.i3ahumblkgpb@charm-u16    | 10.0.0.5 - - [20/Nov/2017 12:56:36] "GET /abc-11216-def HTTP/1.1" 200 -
        abc_server-app.1.i3ahumblkgpb@charm-u16    | 10.0.0.5 - - [20/Nov/2017 12:56:36] "GET /abc-16411-def HTTP/1.1" 200 -
        abc_server-app.1.i3ahumblkgpb@charm-u16    | 10.0.0.5 - - [20/Nov/2017 12:56:36] "GET /abc-25089-def HTTP/1.1" 200 -
        
        $ docker service logs --tail 10  wivmso24yeho
        abc_client-app.1.c6avpy4dk4wq@charm-u16    |   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
        abc_client-app.1.c6avpy4dk4wq@charm-u16    |                                  Dload  Upload   Total   Spent    Left  Speed
        100    26  100    26    0     0   4180      0 --:--:-- --:--:-- --:--:--  4333
        abc_client-app.1.c6avpy4dk4wq@charm-u16    | Hello World - abc-41-def!
        abc_client-app.1.c6avpy4dk4wq@charm-u16    | Mon Nov 20 12:57:52 UTC 2017
        abc_client-app.1.c6avpy4dk4wq@charm-u16    |   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
        abc_client-app.1.c6avpy4dk4wq@charm-u16    |                                  Dload  Upload   Total   Spent    Left  Speed
        100    29  100    29    0     0   4211      0 --:--:-- --:--:-- --:--:--  4833
        abc_client-app.1.c6avpy4dk4wq@charm-u16    | Hello World - abc-17228-def!
        abc_client-app.1.c6avpy4dk4wq@charm-u16    | Mon Nov 20 12:58:01 UTC 2017
        abc_client-app.1.c6avpy4dk4wq@charm-u16    |   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
        abc_client-app.1.c6avpy4dk4wq@charm-u16    |                                  Dload  Upload   Total   Spent    Left  Speed


1. Working with `docker config`

        $ ls
        client/  docker-compose.yml  my_sleep_interval.cfg  server/
        
        $ cat my_sleep_interval.cfg
        5

        $ cat docker-compose.yml
        version: "3.3"
        
        services:
           server-app:
              image: 'shri314/server-app'
              build:
                 context: 'server'
                 dockerfile: 'Dockerfile'
        
           client-app:
              image: 'shri314/client-app'
              build:
                 context: 'client'
                 dockerfile: 'Dockerfile'
              configs:
                 - sleep_interval
        
        configs:
          sleep_interval:
             file: my_sleep_interval.cfg

        $ cat client/ABC.sh
        #!/bin/bash
        
        while [ true ]
        do
           curl server-app:5000/abc-${RANDOM}-def
           date
           sleep $(cat /sleep_interval)     # Now reading from config
        done

        
        $ docker stack deploy --compose-file docker-compose.yml abc
        Ignoring unsupported options: build
        
        Creating network abc_default
        Creating service abc_server-app
        Creating service abc_client-app
        
        $ docker config ls
        ID                          NAME                 CREATED             UPDATED
        021glpue6044xq3e6qxp1oufa   abc_sleep_interval   About an hour ago   About an hour ago

        $ docker ps
        CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS               NAMES
        2679c5ad79ee        shri314/client-app:latest   "/bin/sh -c /root/..."   2 hours ago         Up 2 hours                              abc_client.1.c6avpy4dk4wqkaucxv4st8p3j
        df8dea609d9f        shri314/server-app:latest   "python app.py"          2 hours ago         Up 2 hours                              abc_two_host.1.i3ahumblkgpbfkg9mprli8gfa

        $ docker exec -it 2679c5ad79ee cat '/sleep_interval'
        5


1. Working with `docker secret` - works for the most part exactly like docker config

1. docker stack rm
1. docker swarm leave
