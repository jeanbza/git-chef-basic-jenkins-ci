# git-chef-basic-jenkins-ci
Chef solo scripts to launch a basic jenkins CI on AWS

## Setup

1. Launch an AWS RedHat instance (default as of this writing is RHEL7.1)
1. SSH into newly created instance
1. `sudo yum install git`
1. [Install rbenv via git](https://github.com/sstephenson/rbenv#basic-github-checkout)
  1. Be sure to [install ruby-build](https://github.com/sstephenson/ruby-build#readme) as part of the setup
1. `sudo yum install gcc`
1. `rbenv install 2.1.2` (may take some time)
  1. Note: You may be prompted to install some stuff - go for it, then repeat the `rbenv install 2.1.2`. Example: `sudo yum install -y openssl-devel readline-devel zlib-devel`
1. `rbenv global 2.1.2`
1. `curl -L https://www.opscode.com/chef/install.sh | sudo bash`
1. `git clone https://github.com/jadekler/git-chef-basic-jenkins-ci.git && cd git-chef-basic-jenkins-ci`
1. 
