Vagrant.configure(2) do |config|
	config.vm.define "ansdemo" do |ansdemo|
		ansdemo.vm.box = "generic/oracle9"
		ansdemo.vm.network "forwarded_port", guest: 12500, host: 12500
		ansdemo.vm.provision :shell, inline: "setenforce 0"
	end
end
