
# Deploy Ruby on Rails into an AWS EC2 Instance

```sh
# Connect to your instance from your terminal
ssh -i /path_to_the_file/file_name.pem ubuntu@ip # Public IP From EC2 Instance
# When running this after the first download, it will through an error
# It will say that this instance isn't secure, for that will run
# The following cmd
chmod 400 /Downloads/example-key-1.pem
# Because the Pen file doesn't have the right permission to execute it
# Then will be able to log with the last command
ssh -i /Downloads/example-key-1.pem ubuntu@ip

# Now we need to set up the environment as a normal machine, I'll use rbenv
# So first will update the instance
sudo apt update
sudo apt upgrade

# Then will make sure everything all library to install ruby
sudo apt install gcc make libssl-dev libreadline-dev zlib1g-dev libsqlite3-dev
sudo apt-get install build-essential # For compiling Sass
```

### Rbenv & Ruby basic installation
```sh
# After that will want to clone rbenv (Git comes with these instances)
git clone https://github.com/rbenv/rbenv.git ~/.rbenv

# Add path to our .bashrc
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc

# Let's make sure rails runs only on production in this machine
echo 'export RAILS_ENV=production' >> ~/.bashrc
# ONLY IF YOU WANT TO SEE THE LOG OF YOUR SERVER ADD THIS LINE
# echo 'export RAILS_LOG_TO_STDOUT=true' >> ~/.bashrc  
exit # this so we can reload the terminal

# Connect to your instance from your terminal again
ssh -i /path_to_the_file/file_name.pem ubuntu@ip 

# Next will install the ruby-build (this is encharge of keeping all 
# versions supported by rbenv)
mkdir -p "$(rbenv root)"/plugins
git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build


# Lets make sure we have everything running
rbenv -v
# -> rbenv 1.1.2-2-g4e92322

# Now Will Finally going to install ruby
rbenv install 2.7.2 --verbose

# Let's set it globally
rbenv global 2.7.2

# Let's check is working
ruby -v
# -> ruby 2.7.0pxx (20xx-xx-xx revision xxxxx) [x86_64-linux]
```
### Install yarn
```sh
# Add downloads to our source list
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
# Update and install 
sudo apt update && sudo apt install yarn
# Check is working
yarn --version
# -> 1.22.5
# Install Rails and Bundler
```

### Rails Installation and some and extra commands :wink:
```sh
gem install rails
# Generate a new project or pull the project you want to use
rails new example 

# Compile assets
rails assets:precompile

# RUN SERVER
screen rails s # ctrl-a d to detach screen ---> screen -r # Resume screen
exit
```
