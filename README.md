# The simplest Capistrano file for deploying PHP apps from github.


This project consists of a Capfile and these instructions. Put the Capfile in the root of your project and follow the instructions below. 

##Instructions

### Github Setup

* Create a github account for yourself if you don't have one
* (optional reccomended) Upload your public key to github
    * if you don't have keys you can generate them using ssh-keygen 


### Server setup
4. (optional recommended) Create a deployment user for your app your application will be deployed in this users home directory
4.1. sudo /usr/sbin/useradd app_deployer
5. (optional) if you don't want to type in a password all the time copy your public key to the deploy users ~/.ssh/authorized_keys
5.1. On debian based systems ssh-copy-id works great


###  Setup your workstation
5.  Install ruby (rvm works great on unix systems)
6.  Install rubygems unless your ruby installer already did it for you
7.  install capistrano 
7.1 gem install capistrano


###  Deploy!
7. Put the Capfile in your application's home directory
8. Modify to suit your application and deployment needs.
9. type "cap testing deploy:setup" (substitute production, staging for testing as needed)
10. cap testing deploy
11. cap production deploy
12. cap staging deploy

