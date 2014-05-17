VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box     = "CentOS6.4-i386"
  config.vm.box_url = "http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-i386-v20131103.box"

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  config.vm.provision :shell, inline: <<-EOF
    sudo rpm -i \
      http://yum.puppetlabs.com/puppetlabs-release-el-6.noarch.rpm
    sudo yum install -y puppet
    sudo /sbin/chkconfig --add puppet
    sudo /sbin/chkconfig puppet on
    sudo /etc/init.d/puppet start
  EOF

  config.vm.define :app do |c|
    c.vm.provision :shell do |shell|
      shell.path = "provision.sh"
      shell.args = "app"
    end
  end
end
