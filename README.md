# zabbix-postfix-template
Zabbix template for Postfix SMTP server

Works for Zabbix 5.X

Forked from http://admin.shamot.cz/?p=424

# Requirements
* [pflogsum](http://jimsun.linxnet.com/postfix_contrib.html)
* [pygtail](https://pypi.org/project/pygtail/)

# Installation

Customised for NethServer, probably workable for CentoS, 
    
    # for CentOS
    yum install postfix-perl-scripts
    
    wget https://raw.githubusercontent.com/stephdl/zabbix-postfix-template/master/pygtail.py -O /usr/sbin//pygtail.py
    chmod +x /usr/sbin/pygtail.py
    
    wget https://raw.githubusercontent.com/stephdl/zabbix-postfix-template/master/zabbix-postfix-stats.sh -O /usr/bin/zabbix-postfix-stats.sh
    chmod +x /usr/bin/zabbix-postfix-stats.sh

    # zabbix_agent
    wget https://raw.githubusercontent.com/stephdl/zabbix-postfix-template/master/userparameter_postfix.conf -O /etc/zabbix/zabbix_agentd.d/userparameter_postfix.conf
    or
    # zabbix_agent2
    wget https://raw.githubusercontent.com/stephdl/zabbix-postfix-template/master/userparameter_postfix.conf -O /etc/zabbix/zabbix_agent2.d/userparameter_postfix.conf
    
    # run visudo as root
    Defaults:zabbix !requiretty
    zabbix ALL=NOPASSWD: /usr/bin/zabbix-postfix-stats.sh
    
    systemctl restart zabbix-agent
    or
    systemctl restart zabbix-agent2

Finally import template_app_zabbix.xml and attach it to your host. Go to : https://raw.githubusercontent.com/stephdl/zabbix-postfix-template/master/template_app_zabbix.xml
do a ctrl+s, save the template to your computer and import it with the zabbix UI (/configuration/Templates/import a template)
