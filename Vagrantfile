VAGRANTFILE_API_VERSION = "2"

this_role = 'homework'
this_env = 'dev'

aws_access_key_id = ENV['AWS_ACCESS_KEY_ID']
aws_secret_access_key = ENV['AWS_SECRET_ACCESS_KEY']

ENV['ANSIBLE_CONFIG'] = "ansible/ansible.cfg"
ENV['ANSIBLE_DIR'] = "ansible/"

vagrant_ip = "192.168.52.101"

boxes = {
 "centos7" => "centos/7",
}

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  boxes.each do |distribution, box|
    config.ssh.insert_key = false
    config.ssh.forward_agent = true
  
    config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--cpus", "1"]
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
      vb.customize ["modifyvm", :id, "--nictype1", "virtio" ]
      vb.customize ["modifyvm", :id, "--nictype2", "virtio" ]
    end
  
    config.vm.define "#{distribution}-#{this_role}" do |host|
      host.vm.hostname = this_role
      host.vm.box = box
      host.vm.network :private_network, ip: vagrant_ip
      host.vm.provision "ansible" do |ansible|
        ansible.limit = "all"
        ansible.extra_vars = {
          ENV: this_env,
          aws_access_key: aws_access_key_id,
          aws_secret_key: aws_secret_access_key,
        }
        ansible.playbook = "ansible/homework.yml"
        ansible.compatibility_mode = "2.0"
        ansible.groups = {
          "#{this_role}-#{this_env}" => [ "#{distribution}-#{this_role}" ]
        }
      end
    end
  end
end
