FROM amazonlinux

# set yum repository mirror for jp
RUN rm -f /etc/yum/vars/awsregion; echo 'ap-northeast-1' > /etc/yum/vars/awsregion

# install packages
RUN yum -y update
RUN yum -y install acl acpid alsa-lib ansible at attr audit audit-libs authconfig \
    autogen-libopts aws-amitools-ec2 aws-apitools-as aws-apitools-common aws-apitools-ec2 \
    aws-apitools-elb aws-apitools-mon aws-cfn-bootstrap aws-cli basesystem bash bc bind-libs\
    bind-utils binutils bzip2 bzip2-libs ca-certificates checkpolicy chkconfig cloud-disk-utils \
    cloud-init coreutils cpio cracklib cracklib-dicts cronie cronie-anacron crontabs cryptsetup \
    cryptsetup-libs curl cyrus-sasl cyrus-sasl-lib cyrus-sasl-plain dash db4 db4-utils dbus \
    dbus-libs dejavu-fonts-common dejavu-sans-fonts dejavu-serif-fonts device-mapper \
    device-mapper-event device-mapper-event-libs device-mapper-libs device-mapper-persistent-data \
    dhclient dhcp-common diffutils dmraid dmraid-events dracut dracut-modules-growroot dump \
    e2fsprogs e2fsprogs-libs ec2-net-utils ec2-utils ed elfutils-libelf epel-release ethtool \
    expat file file-libs filesystem findutils fipscheck fipscheck-lib fontconfig \
    fontpackages-filesystem freetype gawk gdbm gdisk generic-logos get_reference_source giflib git \
    glib2 glibc glibc-common gmp gnupg2 gpgme gpm-libs grep groff groff-base grub grubby gzip \
    hesiod hmaccalc hwdata info initscripts iproute iptables iputils irqbalance java-1 \
    javapackages-tools jpackage-utils kbd kbd-misc kernel kernel kernel-tools keyutils \
    keyutils-libs kmod kmod-libs kpartx krb5-libs lcms2 less libICE libSM libX11 libX11-common \
    libXau libXcomposite libXext libXfont libXi libXrender libXtst libacl libaio libassuan libattr \
    libblkid libcap libcap-ng libcgroup libcom_err libcurl libedit libevent libffi libfontenc \
    libgcc48 libgcrypt libgpg-error libgssglue libicu libidn libidn2 libjpeg-turbo libmount \
    libnfsidmap libnih libnl libpipeline libpng libpsl libpwquality libselinux libselinux-utils \
    libsemanage libsepol libss libssh2 libstdc++48 libsysfs libtasn1 libtirpc libudev libunistring \
    libuser libutempter libuuid libverto libxcb libxml2 libxml2-python27 libxslt libyaml logrotate \
    lsof lua lvm2 lvm2-libs mailcap make man-db man-pages mdadm mingetty nano nc ncurses \
    ncurses-base ncurses-libs net-tools newt newt-python27 nfs-utils nspr nss nss-softokn \
    nss-softokn-freebl nss-sysinit nss-tools nss-util ntp ntpdate ntsysv numactl openldap openssh \
    openssh-clients openssh-server openssl p11-kit p11-kit-trust pam pam_ccreds pam_krb5 \
    pam_passwdqc parted passwd pciutils pciutils-libs pcre perl perl-Carp perl-Digest \
    perl-Digest-HMAC perl-Digest-MD5 perl-Digest-SHA perl-Encode perl-Error perl-Exporter \
    perl-File-Path perl-File-Temp perl-Filter perl-Getopt-Long perl-Git perl-HTTP-Tiny \
    perl-PathTools perl-Pod-Escapes perl-Pod-Perldoc perl-Pod-Simple perl-Pod-Usage \
    perl-Scalar-List-Utils perl-Socket perl-Storable perl-TermReadKey perl-Text-ParseWords \
    perl-Time-HiRes perl-Time-Local perl-constant perl-libs perl-macros perl-parent perl-podlators \
    perl-threads perl-threads-shared pinentry pkgconfig policycoreutils popt procmail procps \
    psacct psmisc pth python-crypto2 python-jinja2-26 python-keyczar python26 python26-PyYAML \
    python26-babel python26-backports python26-backports-ssl_match_hostname  python26-crypto \
    python26-ecdsa python26-httplib2 python26-libs python26-markupsafe python26-paramiko \
    python26-pyasn1 python26-setuptools python26-simplejson python26-six python27 python27-PyYAML \
    python27-babel python27-backports python27-backports-ssl_match_hostname  python27-boto \
    python27-botocore python27-chardet python27-colorama python27-configobj python27-crypto \
    python27-daemon python27-dateutil python27-devel python27-docutils python27-ecdsa \
    python27-futures python27-imaging python27-iniparse python27-jinja2 python27-jmespath \
    python27-jsonpatch python27-jsonpointer python27-kitchen python27-libs python27-lockfile \
    python27-markupsafe python27-paramiko python27-pip python27-ply python27-pyasn1 python27-pycurl \
    python27-pygpgme python27-pyliblzma python27-pystache python27-pyxattr python27-requests \
    python27-rsa python27-setuptools python27-simplejson python27-six python27-urlgrabber \
    python27-urllib3 python27-virtualenv quota quota-nls readline rmt rng-tools rootfiles rpcbind \
    rpm rpm-build-libs rpm-libs rpm-python27 rsync rsyslog ruby ruby20 ruby20-irb ruby20-libs \
    rubygem20-bigdecimal rubygem20-json rubygem20-psych rubygem20-rdoc rubygems20 screen sed \
    sendmail setserial setup sgpio shadow-utils shared-mime-info slang sqlite sshpass sudo \
    sysctl-defaults sysfsutils system-release sysvinit tar tcp_wrappers tcp_wrappers-libs tig \
    time tmpwatch traceroute ttmkfdir tzdata tzdata-java udev unzip update-motd upstart ustr \
    util-linux vim-common vim-enhanced vim-filesystem vim-minimal wget which words \
    xorg-x11-font-utils xorg-x11-fonts-Type1 xz xz-libs yum yum-metadata-parser \
    yum-plugin-priorities yum-plugin-upgrade-helper yum-utils zip zlib
RUN yum -y install htop

# create users
RUN useradd -G wheel -m ec2-user
RUN passwd -f -u ec2-user

# setup sudoers
RUN echo "%wheel ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/ec2-user

# setup SSH
RUN mkdir -p /home/ec2-user/.ssh; chown ec2-user /home/ec2-user/.ssh; chmod 700 /home/ec2-user/.ssh
RUN wget https://git.io/ed25519 -O /home/ec2-user/.ssh/authorized_keys
RUN chown ec2-user: /home/ec2-user/.ssh/authorized_keys
RUN chmod 600 /home/ec2-user/.ssh/authorized_keys

# setup sshd config
RUN sed -ri 's/#PermitRootLogin yes/PermitRootLogin yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config

RUN chkconfig --add sshd; chkconfig sshd on; service sshd start;

# replace /sbin/init
RUN wget https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 -O /sbin/dumb-init
RUN chmod +x /sbin/dumb-init

# for compatibility
RUN touch /etc/sysconfig/network

EXPOSE 22
ENTRYPOINT /sbin/dumb-init -- service sshd start; sleep infinity