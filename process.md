Install zabbix-ruby-client with chef installed
===========
    sudo /opt/chef/embedded/bin/gem install zubbix-ruby-client
    zrc init --> This will create a "zabbix-ruby-client" directory in $HOME directory
    mv zabbix-client-ruby/ zabbix
    cd zabbix
    bundle -- to show necessary dependancies and will prompt for zabbix-sender
    vi config.yml --> change "host" to the hostname and "host" under "zabbix" to the hostname of the zabbix server (noc.vpn in this case)
    vi monthly.yml --> modify "name: disk" --> "args" to the "/dev/xxx" that needs to be monitored and modify the network part to the interface(s) needs to be monitored.

    cd zabbix (if not in the directory already)
    zrc show --> will show that zabbix-sender is needed
    
    sudo apt-get install zabbix-sender --> Got an error msg saying that there is no zabbix-sender package found
    
    cd /etc/apt/sources.list.d/ and add zabbix.list file, put the following 2 lines in the file
    
    deb http://repo.zabbix.com/zabbix/2.2/ubuntu precise main
    deb-src http://repo.zabbix.com/zabbix/2.2/ubuntu precise main
    
    sudo apt-get update
    
    sudo apt-get install zabbix-sender --> Got an GPG error saying that the public key is not available: NO_PUBKEY xxxxxxxxxx
    
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys xxxxxxxxx

    sudo apt-get install zabbix-sender --> will succeed this time
    
    make sure you are in zabbix directory and make a "data" directory
    
    mk data
    
    zrc update -t monthly.yml
    
    crontab -e to add scheduled tasks:
    
    * * * * * /bin/bash -l -c "cd $HOME/zabbix && /opt/chef/embedded/bin/bundle exec /opt/chef/embedded/bin/zrc upload"
    0 * * * * /bin/bash -l -c "cd $HOME/zabbix && /opt/chef/embedded/bin/bundle exec /opt/chef/embedded/bin/zrc upload -t hourly.yml"
    0 0 1 * * /bin/bash -l -c "cd $HOME/zabbix && /opt/chef/embedded/bin/bundle exec /opt/chef/embedded/bin/zrc upload -t monthly.yml"

    Modify related yml files like "minutely.yml" if needed
    


