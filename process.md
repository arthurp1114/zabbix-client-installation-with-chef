Install zabbix-ruby-client with chef installed
===========
    sudo /opt/chef/embedded/bin/gem install zubbix-ruby-client
    zrc init --> This will create a "zabbix-ruby-client" directory in $HOME directory
    mv zabbix-client-ruby/ zabbix
    cd zabbix
    bundle -- to show necessary dependancies and will prompt for zabbix-sender
    vi config.yml --> change "host" to the hostname and "host" under "zabbix" to the hostname of the zabbix server (noc.vpn in this case)
    vi monthly.yml --> modify "name: disk" --> "args" to the "/dev/xxx" that needs to be monitored and modify the network part to the interface(s) needs to be monitored.


