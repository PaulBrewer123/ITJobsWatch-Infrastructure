
required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end
Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
    config.omnibus.chef_version = '14.12.9'
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.100"
    app.hostsupdater.aliases = ["development.local"]
    #app.vm.synced_folder "cookbooks/jobswatch_cookbook/files/default/app", "/home/ubuntu/app"
    app.vm.provision "chef_zero" do |chef|
      chef.add_recipe 'jobswatch_cookbook'
      chef.nodes_path = 'cookbooks/jobswatch_cookbook/nodes'
    end
  end
end
