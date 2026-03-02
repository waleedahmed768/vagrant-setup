Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/jammy64"
  config.vm.boot_timeout = 600

  def setup_node(node, name, ip)
    node.vm.hostname = name

    # Bridged adapter
    node.vm.network "public_network" 	

    node.vm.provider "virtualbox" do |vb|
      vb.name = name
      vb.memory = 4096
      vb.cpus = 2
    end

    node.vm.provision "shell", inline: <<-SHELL
      # Set password for vagrant user
      echo "vagrant:vagrant" | sudo chpasswd

    username="ubuntu"
    password="ubuntu"  # set password for the user

    # Check if user exists; if not, create
    if ! id -u $username >/dev/null 2>&1; then
      useradd -m -s /bin/bash $username
      echo "$username:$password" | chpasswd
      usermod -aG sudo $username
    fi

    # Backup the cloud-init file
    cp /etc/cloud/cloud.cfg.d/60-cloudimg-settings.conf /etc/cloud/cloud.cfg.d/60-cloudimg-settings.conf.bak

   sed -i 's/^PasswordAuthentication no/PasswordAuthentication yes/' \
      /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
    # Ensure root login is allowed
    sed -i 's/^#PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config
    sed -i 's/^PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config

    # Restart SSH service to apply changes
    systemctl restart ssh

      # Configure static IP on bridged interface (enp0s8)
      sudo bash -c 'cat > /etc/netplan/01-netcfg.yaml <<EOF
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s8:
      dhcp4: no
      addresses:
        - #{ip}/23
      gateway4: 10.250.30.1
      nameservers:
        addresses:
          - 10.0.0.211
          - 8.8.8.8
EOF'
      sudo netplan apply
    SHELL
  end

  # -------- MASTER-1 --------
  config.vm.define "master-1" do |node|
    setup_node(node, "master-1", "10.250.30.240")
  end

  # -------- MASTER-2 --------
  config.vm.define "master-2" do |node|
    setup_node(node, "master-2", "10.250.30.241")
  end

  # -------- MASTER-3 --------
  config.vm.define "master-3" do |node|
    setup_node(node, "master-3", "10.250.30.242")
  end

end