# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "dummy"
  config.vm.boot_timeout = 600

  config.omnibus.chef_version = :latest

  config.vm.provider :aws do |aws, override|
    aws.access_key_id = ENV["AWS_KEY_ID"]
    aws.secret_access_key = ENV["AWS_SECRET_ACCESS_KEY"]
    aws.keypair_name = "devenv-key"
    aws.security_groups = ["sg-213b2646"]
    aws.subnet_id = "subnet-eca1b69b"
    aws.region = "us-east-1"
    aws.associate_public_ip = true

    aws.instance_type = 'm3.medium'
    aws.ami = "ami-d05e75b8"

    override.ssh.username = "ubuntu"
    override.ssh.private_key_path = "~/.ssh/devenv-key.pem"
  end

  # github ssh key
  config.vm.provision "file", source: "~/.ssh/id_rsa", destination: ".ssh/id_rsa"
  # secrets
  config.vm.provision "file", source: "~/.secrets", destination: ".secrets"

  config.vm.provision "chef_zero" do |chef|
    chef.roles_path = "../azure_development_vm/roles"
    chef.add_role("base")
    chef.add_role("hadoop_nn")
    chef.add_role("hadoop_dn")
    chef.add_role("spark_master")
    chef.add_role("spark_worker")
    chef.add_role("kafka")
    chef.add_role("tachyon_master")
    chef.add_role("tachyon_worker")
  end

end
