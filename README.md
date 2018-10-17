#Created two Aws EC2  t2.micro instances or latest ubuntu 16.04 LTS 

root@MSR-test-Instance-1:~# cat /etc/os-release
NAME="Ubuntu"
VERSION="16.04.5 LTS (Xenial Xerus)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 16.04.5 LTS"
VERSION_ID="16.04"
HOME_URL="http://www.ubuntu.com/"
SUPPORT_URL="http://help.ubuntu.com/"
BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
VERSION_CODENAME=xenial
UBUNTU_CODENAME=xenial
root@MSR-test-Instance-1:~#
root@MSR-test-Instance-1:~# uname -a
Linux MSR-test-Instance-1 4.4.0-1067-aws #77-Ubuntu SMP Mon Aug 27 13:22:03 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
root@MSR-test-Instance-1:~#

root@MSR-test-Instance-2:~#
root@MSR-test-Instance-2:~# cat /etc/os-release
NAME="Ubuntu"
VERSION="16.04.5 LTS (Xenial Xerus)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 16.04.5 LTS"
VERSION_ID="16.04"
HOME_URL="http://www.ubuntu.com/"
SUPPORT_URL="http://help.ubuntu.com/"
BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
VERSION_CODENAME=xenial
UBUNTU_CODENAME=xenial
root@MSR-test-Instance-2:~#
root@MSR-test-Instance-2:~# uname -a
Linux MSR-test-Instance-2 4.4.0-1067-aws #77-Ubuntu SMP Mon Aug 27 13:22:03 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
root@MSR-test-Instance-2:~#

##To make the hostname static  change the configuration in /etc/cloud/cloud.cfg  and change parameter preserve_hostname true and update in /etc/hosts
root@MSR-test-Instance-2:~# cat /etc/cloud/cloud.cfg | grep preserve_hostname
preserve_hostname: true
root@MSR-test-Instance-2:~#

root@MSR-test-Instance-1:~# hostname
MSR-test-Instance-1
root@MSR-test-Instance-1:~#
root@MSR-test-Instance-2:~# hostname
MSR-test-Instance-2
root@MSR-test-Instance-2:~#


# The build-essential dependency packages need to be installed  for setting up nvm

# apt-get install build-essential libssl-dev
# curl https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
root@MSR-test-Instance-2:~# nvm --version
0.33.2
root@MSR-test-Instance-2:~#


root@MSR-test-Instance-2:~# curl -sL https://deb.nodesource.com/setup_8.x  -o nodesource_setup.sh
root@MSR-test-Instance-2:~# ls
nodesource_setup.sh  snap
root@MSR-test-Instance-2:~#
root@MSR-test-Instance-2:~# bash nodesource_setup.sh
root@MSR-test-Instance-2:~# apt-get install -y nodejs
root@MSR-test-Instance-2:~# node -v
v8.12.0
root@MSR-test-Instance-2:~# nodejs -v
v8.12.0
root@MSR-test-Instance-2:~#

# installing Docker 18.06 version 
root@MSR-test-Instance-1:~# apt-get install apt-transport-https ca-certificates curl software-properties-common
root@MSR-test-Instance-1:~# curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
OK
root@MSR-test-Instance-1:~# add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
root@MSR-test-Instance-1:~# cat /etc/apt/sources.list | grep docker
deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable
# deb-src [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable
root@MSR-test-Instance-1:~#
root@MSR-test-Instance-1:~# apt-get update
root@MSR-test-Instance-1:~# apt-cache policy docker-ce
root@MSR-test-Instance-1:~# apt-get install docker-ce=18.06.1~ce~3-0~ubuntu
root@MSR-test-Instance-1:~# systemctl status docker.service
root@MSR-test-Instance-1:~# systemctl start docker.service
root@MSR-test-Instance-1:~# systemctl enable docker.service
root@MSR-test-Instance-1:~# docker -v
Docker version 18.06.1-ce, build e68fc7a
root@MSR-test-Instance-1:~#
root@MSR-test-Instance-1:~# docker version

## installing Docker compose 1.18 version 
root@MSR-test-Instance-1:~# curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
root@MSR-test-Instance-1:~# chmod +x /usr/local/bin/docker-compose
root@MSR-test-Instance-1:~# docker-compose --version
docker-compose version 1.18.0, build 8dd22a9
root@MSR-test-Instance-1:~#


## Installing the latest openssl package 
root@MSR-test-Instance-1:~# apt install build-essential checkinstall zlib1g-dev -y
root@MSR-test-Instance-1:~# cd /usr/src
root@MSR-test-Instance-1:/usr/src# wget https://www.openssl.org/source/openssl-1.1.1.tar.gz
--2018-10-17 19:07:49--  https://www.openssl.org/source/openssl-1.1.1.tar.gz
Resolving www.openssl.org (www.openssl.org)... 23.59.197.23, 2600:1409:0:593::c1e, 2600:1409:0:597::c1e
Connecting to www.openssl.org (www.openssl.org)|23.59.197.23|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 8337920 (8.0M) [application/x-gzip]
Saving to: ‘openssl-1.1.1.tar.gz’

openssl-1.1.1.tar.gz                          100%[==============================================================================================>]   7.95M  1.50MB/s    in 5.0s

2018-10-17 19:07:56 (1.59 MB/s) - ‘openssl-1.1.1.tar.gz’ saved [8337920/8337920]

root@MSR-test-Instance-1:/usr/src#
root@MSR-test-Instance-1:/usr/src# tar -xvf openssl-1.1.1.tar.gz
root@MSR-test-Instance-1:/usr/src/openssl-1.1.1# ls
ACKNOWLEDGEMENTS  AUTHORS     config          Configure     demos    e_os.h    fuzz     LICENSE  NOTES.ANDROID  NOTES.UNIX  os-dep         README.FIPS  tools
apps              build.info  config.com      CONTRIBUTING  doc      external  include  ms       NOTES.DJGPP    NOTES.VMS   README         ssl          util
appveyor.yml      CHANGES     Configurations  crypto        engines  FAQ       INSTALL  NEWS     NOTES.PERL     NOTES.WIN   README.ENGINE  test         VMS
root@MSR-test-Instance-1:/usr/src/openssl-1.1.1# ./config
root@MSR-test-Instance-1:/usr/src/openssl-1.1.1# make
root@MSR-test-Instance-1:/usr/src/openssl-1.1.1# make test
root@MSR-test-Instance-1:/usr/src/openssl-1.1.1# make install

root@MSR-test-Instance-1:/usr/local/src/openssl-1.0.2o# openssl  version -a
OpenSSL 1.0.2g  1 Mar 2016
built on: reproducible build, date unspecified
platform: debian-amd64
options:  bn(64,64) rc4(16x,int) des(idx,cisc,16,int) blowfish(idx)
compiler: cc -I. -I.. -I../include  -fPIC -DOPENSSL_PIC -DOPENSSL_THREADS -D_REENTRANT -DDSO_DLFCN -DHAVE_DLFCN_H -m64 -DL_ENDIAN -g -O2 -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -Wl,-Bsymbolic-functions -Wl,-z,relro -Wa,--noexecstack -Wall -DMD32_REG_T=int -DOPENSSL_IA32_SSE2 -DOPENSSL_BN_ASM_MONT -DOPENSSL_BN_ASM_MONT5 -DOPENSSL_BN_ASM_GF2m -DSHA1_ASM -DSHA256_ASM -DSHA512_ASM -DMD5_ASM -DAES_ASM -DVPAES_ASM -DBSAES_ASM -DWHIRLPOOL_ASM -DGHASH_ASM -DECP_NISTZ256_ASM
OPENSSLDIR: "/usr/lib/ssl"
root@MSR-test-Instance-1:/usr/local/src/openssl-1.0.2o#


## installing Git package
root@MSR-test-Instance-1:~# apt-get install git -y
root@MSR-test-Instance-1:~# git version
git version 2.7.4
root@MSR-test-Instance-1:~#




