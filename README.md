# git-chef-basic-jenkins-ci
Chef solo scripts to launch a basic jenkins CI on AWS.

This sets up a build running java unit tests and ruby rspec tests, but you can
and absolutely should mess with this in your own fork to whatever suits your needs!

## Initial Setup

1. Launch an AWS RedHat instance (default as of this writing is RHEL7.1)
1. Open ports 22 (SSH), 80 (HTTP), and 9090 (jenkins) to inbound in your AWS security group settings
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
1. [Install berkshelf](https://downloads.chef.io/chef-dk/redhat/#/) (steps below to save you time)
  1. `sudo yum install wget`
  1. `wget https://opscode-omnibus-packages.s3.amazonaws.com/el/7/x86_64/chefdk-0.7.0-1.el7.x86_64.rpm`
  1. `sudo rpm -Uvh chefdk-0.7.0-1.el7.x86_64.rpm`
1. `berks install && berks vendor cookbooks/`
1. `sudo chef-solo -c solo.rb -j runlist.json`
1. Navigate to `your.instance.ip.address:9090`. You're done!
1. (optional) Assign an elastic IP to your instance so that the address does not periodically change

## Subsequent Reprovisioning

1. SSH into your instance
1. `cd git-chef-basic-jenkins-ci && git pull && sudo chef-solo -c solo.rb -j runlist.json`

## Some notes

- The ruby recipes could probably be removed because it's part of the setup, but
I figure this repo might be useful in a Vagrant setup, which that would not have
been installed ahead of time. Feel free to remove in your own setup or fork.
- Echoing things into bash_profile is pretty terrible. Will remove at some point
unless someone beats me to it with a PR.

## Feedback and suggestions

Please feel free to submit issues and pull requests, or email me at [jadekler@gmail.com](jadekler@gmail.com).
