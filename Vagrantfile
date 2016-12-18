Vagrant.configure('2') do |config|
  config.vm.box = 'dummy'
  config.vm.box_url = 'https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box'

  config.user.defaults = {
      'aws' => {
          'ami' => 'ami-b73b63a0',
          'username' => 'ec2-user',
          'private_key_path' => '~/.ssh/id_rsa',
          'instance_type' => 't2.medium'
      }
  }

  config.vm.provider :aws do |aws, override|
    aws.access_key_id = config.user.aws.access_key_id
    aws.secret_access_key = config.user.aws.secret_access_key
    aws.keypair_name = config.user.aws.keypair_name
    aws.instance_type = config.user.aws.instance_type
    aws.subnet_id = config.user.aws.subnet_id
    aws.security_groups = config.user.aws.security_groups

    aws.ami = config.user.aws.ami

    override.ssh.username = config.user.aws.username
    override.ssh.private_key_path = config.user.aws.private_key_path
  end

  config.vm.provision 'ansible_local' do |a|
    a.sudo = true
    a.playbook = 'vagrant.yml'
    a.galaxy_role_file = 'requirements.yml'
    a.verbose = 'vv'
  end
end