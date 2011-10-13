# The simplest Capistrano file for deploying PHP apps from github.


This project consists of a Capfile and these instructions. Put the Capfile in the root of your project and follow the instructions below. 

##Instructions

### Github Setup

* Create a github account for yourself if you don't have one
* (optional reccomended) Upload your public key to github
    * if you don't have keys you can generate them using ssh-keygen see gihub help for instructions


### Server setup
*  (optional recommended) Create a deployment user for your app your application will be deployed in this users home directory
    * sudo /usr/sbin/useradd app_deployer
* (optional) if you don't want to type in a password all the time copy your public key to the deploy users ~/.ssh/authorized_keys
    * On debian based systems ssh-copy-id works great


###  Setup your workstation
*  Install ruby (rvm works great on unix systems)
*  Install rubygems unless your ruby installer already did it for you
*  install capistrano 
  * gem install capistrano


###  Deploy!
*  Put the Capfile in your application's home directory
*  Modify to suit your application and deployment needs.
*  type "cap testing deploy:setup" (substitute production, staging for testing as needed)
* cap testing deploy
  * cap production deploy
  * cap staging deploy

