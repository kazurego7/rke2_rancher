vm_spec = [
  # rancher #1
  { name: 'rancher-0', cpu: 3, memory: 3072,
    box: 'ubuntu/bionic64',
    private_ip: '192.168.33.100',
    storage: '15GB',
    comment: 'rancher-0' },
  # downstream control plane #1
  { name: 'rancher-1', cpu: 2, memory: 3072,
    box: 'ubuntu/bionic64',
    private_ip: '192.168.33.101',
    storage: '15GB',
    comment: 'rancher-1' },
  # downstream control plane #2
  { name: 'rancher-2', cpu: 2, memory: 3072,
    box: 'ubuntu/bionic64',
    private_ip: '192.168.33.102',
    storage: '15GB',
    comment: 'rancher-2' },
  # downstream control plane #3
  { name: 'rancher-3', cpu: 2, memory: 3072,
    box: 'ubuntu/bionic64',
    private_ip: '192.168.33.103',
    storage: '15GB',
    comment: 'rancher-2' },
  # downstream load balancer #4
  { name: 'lb-0', cpu: 2, memory: 1024,
    box: 'ubuntu/bionic64',
    private_ip: '192.168.33.104',
    storage: '15GB',
    comment: 'lb-0' },
  # downstream worker #1
  { name: 'worker-1', cpu: 2, memory: 1024,
    box: 'ubuntu/bionic64',
    private_ip: '192.168.33.201',
    storage: '15GB',
    comment: 'worker-1' },
  # downstream worker #2
  { name: 'worker-2', cpu: 2, memory: 1024,
    box: 'ubuntu/bionic64',
    private_ip: '192.168.33.202',
    storage: '15GB',
    comment: 'worker-2' },
]




Vagrant.configure('2') do |config|
  vm_spec.each do |spec|
    config.vm.define spec[:name] do |server|
      server.vm.box = spec[:box]
      server.disksize.size = spec[:storage]
      server.vm.box_url = spec[:box_url]
      server.vm.hostname = spec[:name]
      server.vm.network :private_network, ip: spec[:private_ip]
      server.vm.provider 'virtualbox' do |vbox|
        vbox.gui = false
        vbox.cpus = spec[:cpu]
        vbox.memory = spec[:memory]
      end
    end
  end
  config.vm.provision 'file', source: '~/.ssh/id_rsa.pub', destination: '/tmp/id_rsa.pub'
  config.vm.provision 'shell', inline: 'cat /tmp/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys'
end
