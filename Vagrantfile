Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.provider "virtualbox" do |vb|
     vb.memory = "2048"
  end
  config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update
     sudo apt-get install -y openjdk-7-jdk
     sudo apt-get install -y maven unzip
     cd /vagrant
     curl https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/galagosearch/galagosearch-1.04-src.zip > galagosearch-1.04-src.zip
     unzip galagosearch-1.04-src.zip
     cd galagosearch-1.04
     mkdir corpus
     cd corpus
     curl http://dg3rtljvitrle.cloudfront.net/wiki-small.corpus > wiki-small.corpus
     cd ..
     mvn package
     chmod +x ./galagosearch-core/target/appassembler/bin/galago
     ./galagosearch-core/target/appassembler/bin/galago build corpus/wiki-small.index corpus/wiki-small.corpus
SHELL
end
