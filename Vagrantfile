# -*- mode: ruby -*-
# vi: set ft=ruby :

# -*- mode: ruby -*-
# vi: set ft=ruby :

vms = {
  'srv01-ubuntu' => {'memory' => '1024', 'cpus' => 1, 'ip' => '110', 'box' => 'ubuntu/focal64',},
  'srv02-centos' => {'memory' => '1024', 'cpus' => 1, 'ip' => '220', 'box' => 'centos/7',},
}

Vagrant.configure("2") do |config|

  config.vm.box_check_update = false

  vms.each do |name, conf|
    config.vm.define "#{name}" do |a|
      a.vm.box = "#{conf['box']}"
      a.vm.network 'private_network', ip: "192.168.57.#{conf['ip']}"
      a.vm.hostname = "#{name}"
      a.vm.provider 'virtualbox' do |vb|
        vb.memory = conf['memory']
        vb.cpus = conf['cpus']
        vb.name = "#{name}"
      end
      a.vm.provider 'libvirt' do |lv|
        lv.memory = conf['memory']
        lv.cpus = conf['cpus']
        lv.cputopology :sockets => 1, :cores => conf['cpus'], :threads => '1'
      end
    end
  end
end