
Vagrant.configure("2") do |config|

        # machine1
       	config.vm.define "machine1" do |machine1|
                machine1.vm.hostname = "machine1"
               	machine1.vm.box = "hashicorp/bionic64"
                machine1.vm.network "public_network", ip: "192.168.1.141"
               	machine1.vm.provider "virtualbox" do |vb|
                       	vb.customize ["modifyvm", :id, "--memory", "2048" ]
                       	vb.customize ["modifyvm", :id, "--cpus", "1" ]
                       	vb.customize ["modifyvm", :id, "--name", "machine1" ]
               	end
               	machine1.vm.provision "shell", inline: <<-SHELL
               	sudo echo "192.168.1.141 machine1" | sudo tee -a /etc/hosts
               	sudo echo "192.168.1.142 machine2" | sudo tee -a /etc/hosts
               	sudo echo "192.168.1.143 machine3" | sudo tee -a /etc/hosts
               	sudo apt update
               	sudo apt upgrade
		sudo apt install rabbitmq-server -y
		sudo systemctl start rabbitmq-server
		sudo systemctl enable rabbitmq-server
                sudo rabbitmq-plugins enable rabbitmq_management
		sudo systemctl restart rabbitmq-server
        	sudo ufw allow ssh
		sudo ufw enable
		sudo ufw allow 5672,15672,4369,25672/tcp
 		sudo cp /var/lib/rabbitmq/.erlang.cookie /vagrant/
               	SHELL
       	end

        # machine2
        config.vm.define "machine2" do |machine2|
                machine2.vm.hostname = "machine2"
                machine2.vm.box = "hashicorp/bionic64"
                machine2.vm.network "public_network", ip: "192.168.1.142"
                machine2.vm.provider "virtualbox" do |vb|
                        vb.customize ["modifyvm", :id, "--memory", "2048" ]
                        vb.customize ["modifyvm", :id, "--cpus", "1" ]
                        vb.customize ["modifyvm", :id, "--name", "machine2" ]
                end
                machine2.vm.provision "shell", inline: <<-SHELL
                sudo echo "192.168.1.141 machine1" | sudo tee -a /etc/hosts
                sudo echo "192.168.1.142 machine2" | sudo tee -a /etc/hosts
                sudo echo "192.168.1.143 machine3" | sudo tee -a /etc/hosts
                sudo apt update
                sudo apt upgrade
                sudo apt install rabbitmq-server -y
                sudo systemctl start rabbitmq-server
                sudo systemctl enable rabbitmq-server
                sudo rabbitmq-plugins enable rabbitmq_management
                sudo systemctl restart rabbitmq-server
                sudo ufw allow ssh
                sudo ufw enable
                sudo ufw allow 5672,15672,4369,25672/tcp
                sudo cp /vagrant/.erlang.cookie /var/lib/rabbitmq/
                sudo rm -rf /var/log/rabbitmq/*
                sudo systemctl restart rabbitmq-server
		sudo rabbitmqctl stop_app
		sudo rabbitmqctl join_cluster rabbit@machine1
		sudo rabbitmqctl start_app
                SHELL
        end

        # machine3
        config.vm.define "machine3" do |machine3|
                machine3.vm.hostname = "machine3"
                machine3.vm.box = "hashicorp/bionic64"
                machine3.vm.network "public_network", ip: "192.168.1.143"
                machine3.vm.provider "virtualbox" do |vb|
                        vb.customize ["modifyvm", :id, "--memory", "2048" ]
                        vb.customize ["modifyvm", :id, "--cpus", "1" ]
                        vb.customize ["modifyvm", :id, "--name", "machine3" ]
                end
                machine3.vm.provision "shell", inline: <<-SHELL
                sudo echo "192.168.1.141 machine1" | sudo tee -a /etc/hosts
                sudo echo "192.168.1.142 machine2" | sudo tee -a /etc/hosts
                sudo echo "192.168.1.143 machine3" | sudo tee -a /etc/hosts
                sudo apt update
                sudo apt upgrade
                sudo apt install rabbitmq-server -y
                sudo systemctl start rabbitmq-server
                sudo systemctl enable rabbitmq-server
                sudo rabbitmq-plugins enable rabbitmq_management
                sudo systemctl restart rabbitmq-server
                sudo ufw allow ssh
                sudo ufw enable
                sudo ufw allow 5672,15672,4369,25672/tcp
                sudo cp /vagrant/.erlang.cookie /var/lib/rabbitmq/
                sudo rm -rf /var/log/rabbitmq/*
                sudo systemctl restart rabbitmq-server
                sudo rabbitmqctl stop_app
                sudo rabbitmqctl join_cluster rabbit@machine1
                sudo rabbitmqctl start_app
   		sudo rabbitmqctl set_policy ha-all ".*" '{"ha-mode":"all"}'
                sudo rabbitmqctl add_user dmitry 123456
		sudo rabbitmqctl set_user_tags dmitry administrator
		sudo rabbitmqctl set_permissions -p / dmitry ".*" ".*" ".*"
                SHELL
        end
end
