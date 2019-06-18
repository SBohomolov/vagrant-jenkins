ENV["LC_ALL"] = "en_US.UTF-8"

$script = <<-EOF
export LC_ALL=en_US.UTF-8
sudo yum -y update
sudo yum -y install wget
sudo cp /vagrant/jenkins/nginx.repo /etc/yum.repo.d/nginx.repo
sudo cp /vagrant/jenkins/default.conf /etc/sysconfig/default.conf
sudo cp /vagrant/jenkins/jenkins /etc/sysconfig/jenkins
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
#sudo wget -O /etc/yum.repos.d/nginx.repo https://raw.githubusercontent.com/zulus911/lectures/master/lecture2/nginx.repo
sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
sudo yum -y install jenkins nginx net-tools policycoreutils-python java mc htop vim
#sudo wget -O /etc/sysconfig/jenkins https://raw.githubusercontent.com/zulus911/lectures/master/lecture2/jenkins
#sudo wget -O /etc/nginx/conf.d/default.conf https://raw.githubusercontent.com/zulus911/lectures/master/lecture2/default.conf
sudo service jenkins start
sudo service nginx start
EOF

Vagrant.configure("2") do |config|
  config.vm.define "test-vagrant" do |test|
    test.vm.box = "centos/7"
    test.vm.hostname = "stan.box"
    test.vm.network "forwarded_port", guest: "80", host: "80"
    test.vm.network "forwarded_port", guest: "8080", host:"8080"
    test.vm.network "private_network", ip: "172.128.1.2"
    test.vm.network "public_network", type: "dhcp", bridge: 'wlp2s0: Wi-Fi (AirPort)'


    test.vm.provision "shell", inline: $script
  end
end

