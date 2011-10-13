load 'deploy' if respond_to?(:namespace) # cap2 differentiator
Dir['vendor/gems/*/recipes/*.rb','vendor/plugins/*/recipes/*.rb'].each { |plugin| load(plugin) }

default_run_options[:pty] = true

set :application, "your_app_name"
set :repository,  "git@github.com:your_app/your_app.git"
set :scm, :git
set :deploy_via, :remote_cache
set :use_sudo, false

# Uncomment if you are using submodules
#set :git_enable_submodules, 1




# I normally like to forward the ssh agent. This way you don't have to worry about 
# uploading deployment keys to github
# On ubuntu ssh-agent runs by default in the gnome session.
# ssh-agent is also on by default in later versions of MacOSX
# you might have to run ssh-add ~/.ssh/id_rsa on some operating systems.
# http://www.unixwiz.net/techtips/ssh-agent-forwarding.html

set :ssh_options, { :forward_agent => true }
 
# Uncomment if you are not using keys.
#set :user, "app_deployer"  # The server's user for deploys
#set :scm_passphrase, "*GITHUB ACCOUNT PASSWORD*"  
#set :scm_username, '*GITHUB ACCOUNT NAME*'


# uncomment the following line if you want to run ssh-add from here
# it is better to run it from your .bashrc 
# `ssh-add ~/.ssh/id_rsa`


### These are global settings for all environments


##   In this case everything is on one server you can define multiple servers
##  three anyway for future use

production_server = "127.0.0.1"
staging_server = "127.0.0.1"
test_server = "127.0.0.1"

# You are probably using a non standard ssh port right?
set :port, 9922

# this is the deployment user. You will be logging into the server as this user
# the checkout will be done as you via key forwarding.
set :user, "app_deployer"
 
# Adjust the branches and final paths below to suit your needs

task :production do
  set :branch, "master"
  server production_server, :app, :web, :db, :primary => true
  
  #or you can split them like this...
  #role :app, [array, of, servers]
  #role :web, production_server
  #role :db,  production_server, :primary => true
end


task :staging do  
  set :branch, "staging"
  server staging_server, :app, :web, :db, :primary => true
 end

task :testing do   
  set :branch, "staging"
  server testing_server, :app, :web, :db, :primary => true  
  
  #override the default deployment path
  set :deploy_to, "/home/#{user}/#{application}/test"   
                                                                                                                                                                                                   
end



namespace :deploy do
 
  task :finalize_update do
     #need to override this because it does rails specific symlinking.
     # you can add your own symlinking here I am using the #{releases_path} and #{release_name} as an example
     #  could have used #{release_path} 
      transaction do
        run "chmod -R g+w #{releases_path}/#{release_name}"
      end
  end
  
  #override the following because they are not applicable to this app
  task :migrate do ;  end
  task :migrations do ; end
  task :cold do ;  end
  task :start do ;  end
  task :stop do ;  end
  task :restart do;  end
  
  #custom tasks
  task :hello_world, :roles => [:db, :app] do
    puts "calling hello_world..."
    hello_world
  end

end


#note the use of the "before" hook to set the deploy path.

before "deploy" do
  #this is the default deployment directory, you can override in your stages
   set :deploy_to, "/home/#{user}/#{application}/#{branch}" if deploy_to.nil?
end

#examples of using after hook


after "deploy:update_code" do
  deploy.hello_world
end

