# vagrant-centos-rails

Vagrantfile to spin up a rails environment and sample Devise/Bootcamp app from RailsApp for getting started with rails development.


# Usage
    git clone --recursive -j8 git@github.com:kronarq/vagrant-centos-rails.git
    cd vagrant-centos-rails/
    vagrant up

# Other
You can fork https://github.com/kronarq/rails-devise/ and update the submodule to point to your fork.
```
cd vagrant-centos-rails/rails/rails-devise
git remote add upstream git@github.com:USERNAME/rails-devise.git
```
Or you can create your apps in vagrant-centos-rails/rails and update the Vagrantfile to start the server in that directory.
