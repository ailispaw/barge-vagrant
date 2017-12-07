# coding: utf-8
Vagrant.configure("2") do |config|
  config.vm.box = "ailispaw/barge"
  config.vm.network :private_network, ip: "192.168.33.111" # IPアドレス固定
  config.vm.synced_folder "./vm", "/home/bargee/vm", mount_options: ['dmode=755','fmode=755'] # vmフォルダを同期する

  # Dockerのバージョンを最新(v17.09.0-ce)に切り替えて、
  config.vm.provision :shell, inline: <<-SHELL
    /etc/init.d/docker restart v17.09.0-ce
  SHELL

  # nginxのコンテナを作成・起動する。
  config.vm.provision :docker do |docker|
    docker.build_image "/home/bargee/vm/nginx", args: "-t nginx1"
    docker.run "c_nginx1_1",
      image: "nginx1",
      args: "-p 80:80"
  end
end
