# -*- mode: ruby -*-
# vi: set ft=ruby :
$script = <<SCRIPT

apt-get -y update

# APTs
apt-get -y install blt cloud-utils curl dnsmasq-utils docutils-common docutils-doc erlang-asn1 erlang-base erlang-corba erlang-crypto erlang-dev erlang-diameter erlang-docbuilder erlang-edoc erlang-erl-docgen erlang-eunit erlang-ic erlang-inets erlang-inviso erlang-mnesia erlang-nox erlang-odbc erlang-os-mon erlang-parsetools erlang-percept erlang-public-key erlang-runtime-tools erlang-snmp erlang-ssh erlang-ssl erlang-syntax-tools erlang-tools erlang-webtool erlang-xmerl euca2ools fontconfig-config genisoimage iptables iputils-arping javascript-common kpartx libblas3gf libc-ares2 libconfig-general-perl libcurl3 libdbd-mysql-perl libdbi-perl libev4 libexpat1 libexpat1-dev libfontconfig1 libfontenc1 libgfortran3 libgl1-mesa-dri libgl1-mesa-glx libglapi-mesa libhtml-template-perl libibverbs1 libice6 libicu48 libjpeg8 libjpeg-turbo8 libjs-jquery libjs-jquery-metadata libjs-jquery-tablesorter libjs-sphinxdoc libjs-underscore liblapack3gf liblcms1 libldap-2.4-2 libldap2-dev libllvm3.0 libltdl7 liblua5.1-0 libmysqlclient18 libnet-daemon-perl libodbc1 libpaper1 libpaper-utils libperl5.14 libplrpc-perl librdmacm1 libreadline5 libruby1.8 libsasl2-2 libsasl2-dev libsasl2-modules libsctp1 libsgutils2-2 libsm6 libsqlite3-0 libsysfs2 libterm-readkey-perl libtidy-0.99-0 libutempter0 libv8-3.7.12.22 libx11-xcb1 libxaw7 libxcb-glx0 libxcb-shape0 libxcomposite1 libxdamage1 libxfixes3 libxft2 libxi6 libxinerama1 libxml2 libxml2-dev libxmu6 libxpm4 libxrender1 libxslt1.1 libxss1 libxt6 libxtst6 libxv1 libxxf86dga1 libxxf86vm1 libyaml-0-2 lksctp-tools locate lvm2 msgpack-python nodejs open-iscsi open-iscsi-utils openssh-client openssh-server openssl parted perl perl-base perl-modules psmisc pylint python python2.7-dev python-amqplib python-anyjson python-beautifulsoup python-boto python-carrot python-cheetah python-cherrypy3 python-cmd2 python-coverage python-crypto python-dateutil python-decorator python-dev python-dingus python-docutils python-egenix-mxdatetime python-egenix-mxtools python-eventlet python-feedparser python-formencode python-gflags python-greenlet python-imaging python-iso8601 python-jinja2 python-kombu python-libxml2 python-lockfile python-logilab-astng python-logilab-common python-lxml python-m2crypto python-markupsafe python-migrate python-minimal python-mox python-mysqldb python-netaddr python-nose python-numpy python-openid python-openssl python-paramiko python-paste python-pastedeploy python-pastescript python-pip python-pkg-resources python-pygments python-pysqlite2 python-qpid python-roman python-routes python-scgi python-setuptools python-sphinx python-sqlalchemy python-sqlalchemy-ext python-stompy python-suds python-support python-tempita python-tk python-unittest2 python-utidylib python-virtualenv python-webob python-xattr python-yaml rabbitmq-server screen sg3-utils socat sphinx-common sphinx-doc sqlite3 sudo sysfsutils tcl8.5 tgt tk8.5 ttf-dejavu-core unzip vim-common vim-nox vim-runtime vim-tiny vlan wwwconfig-common x11-common x11-utils xbitmaps xterm 
apt-get -y install git apache2 apache2.2-bin apache2.2-common apache2-mpm-worker apache2-utils cgroup-lite cpu-checker kvm kvm-ipxe libapache2-mod-wsgi libapparmor1 libapr1 libaprutil1 libaprutil1-dbd-sqlite3 libaprutil1-ldap libasyncns0 libavahi-client3 libavahi-common3 libavahi-common-data libcaca0 libflac8 libjson0 libnuma1 libogg0 libpulse0 libsdl1.2debian libsndfile1 libvirt0 libvirt-bin libvorbis0a libvorbisenc2 libxenstore3.0 libxml2-utils libyajl1 msr-tools python-libvirt qemu-common qemu-kvm seabios ssl-cert vgabios emacs23-nox
apt-get -y install libxml2-dev libxslt-dev libmysqlclient-dev


su vagrant -c 'cd ~vagrant; git clone git://github.com/openstack-dev/devstack.git'
su vagrant -c 'cp -f /vagrant/localrc ~/devstack'

mkdir /opt/stack
chown vagrant:vagrant /opt/stack
#cd /opt/stack/nova
#su vagrant -c 'git remote add bh git://github.com/holzman/nova.git'
#su vagrant -c 'git fetch bh'

#euca2ools
#su vagrant -c 'cd && git clone git://github.com/eucalyptus/euca2ools'
#cd ~vagrant/euca2ools && python setup.py install
#python /vagrant/ez_setup.py

su vagrant -c 'cd ~/devstack && ./stack.sh'
#echo "OS_USERNAME=admin keystone tenant-list" >> /tmp/tl
#su vagrant -c 'cd /opt/stack/tempest && testr run --parallel'

for pw in ADMIN_PASSWORD MYSQL_PASSWORD RABBIT_PASSWORD SERVICE_PASSWORD SERVICE_TOKEN
do
    echo $pw=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1) >> ~vagrant/devstack/localrc
done

SCRIPT

Vagrant.configure("2") do |config|
#  config.vm.box = "devstack-extra-2014"
  config.vm.box = "precise64"
  config.vm.provision :shell, :inline => $script

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  # config.vm.box_url = "http://domain.com/path/to/above.box"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network :forwarded_port, guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
#  config.vm.network :public_network
#  config.vm.network :private_network, ip: "10.0.2.15"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network :public_network

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider :virtualbox do |vb|
    # Don't boot with headless mode
    # Use VBoxManage to customize the VM. For example to change memory:
     vb.customize ["modifyvm", :id, "--memory", "16384"]
     vb.customize ["modifyvm", :id, "--cpus", "4"]
  end
  config.vm.network :private_network, ip: "171.15.19.31"
  #
  # View the documentation for the provider you're using for more
  # information on available options.

  # Enable provisioning with Puppet stand alone.  Puppet manifests
  # are contained in a directory path relative to this Vagrantfile.
  # You will need to create the manifests directory and a manifest in
  # the file base.pp in the manifests_path directory.
  #
  # An example Puppet manifest to provision the message of the day:
  #
  # # group { "puppet":
  # #   ensure => "present",
  # # }
  # #
  # # File { owner => 0, group => 0, mode => 0644 }
  # #
  # # file { '/etc/motd':
  # #   content => "Welcome to your Vagrant-built virtual machine!
  # #               Managed by Puppet.\n"
  # # }
  #
  # config.vm.provision :puppet do |puppet|
  #   puppet.manifests_path = "manifests"
  #   puppet.manifest_file  = "init.pp"
  # end

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  # config.vm.provision :chef_solo do |chef|
  #   chef.cookbooks_path = "../my-recipes/cookbooks"
  #   chef.roles_path = "../my-recipes/roles"
  #   chef.data_bags_path = "../my-recipes/data_bags"
  #   chef.add_recipe "mysql"
  #   chef.add_role "web"
  #
  #   # You may also specify custom JSON attributes:
  #   chef.json = { :mysql_password => "foo" }
  # end

  # Enable provisioning with chef server, specifying the chef server URL,
  # and the path to the validation key (relative to this Vagrantfile).
  #
  # The Opscode Platform uses HTTPS. Substitute your organization for
  # ORGNAME in the URL and validation key.
  #
  # If you have your own Chef Server, use the appropriate URL, which may be
  # HTTP instead of HTTPS depending on your configuration. Also change the
  # validation key to validation.pem.
  #
  # config.vm.provision :chef_client do |chef|
  #   chef.chef_server_url = "https://api.opscode.com/organizations/ORGNAME"
  #   chef.validation_key_path = "ORGNAME-validator.pem"
  # end
  #
  # If you're using the Opscode platform, your validator client is
  # ORGNAME-validator, replacing ORGNAME with your organization name.
  #
  # If you have your own Chef Server, the default validation client name is
  # chef-validator, unless you changed the configuration.
  #
  #   chef.validation_client_name = "ORGNAME-validator"
end
