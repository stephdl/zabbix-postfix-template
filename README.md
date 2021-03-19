# zabbix-postfix-template
Zabbix template for Postfix SMTP server

Works for Zabbix 5.X

Forked from http://admin.shamot.cz/?p=424

# Requirements
* [pflogsum](http://jimsun.linxnet.com/postfix_contrib.html)
* [pygtail](https://pypi.org/project/pygtail/)

# Installation

Customised for NethServer, probably workable for CentoS

In the host running the zabbix-agent to monitor, please perform the command below

    # for NethServer
    yum install postfix-perl-scripts

    # Dowload and chmod the backend script
    wget https://raw.githubusercontent.com/stephdl/zabbix-postfix-template/master/pygtail.py -O /usr/sbin//pygtail.py && chmod +x /usr/sbin/pygtail.py
    wget https://raw.githubusercontent.com/stephdl/zabbix-postfix-template/master/zabbix-postfix-stats.sh -O /usr/bin/zabbix-postfix-stats.sh && chmod +x /usr/bin/zabbix-postfix-stats.sh

    # If you use zabbix_agent
    wget https://raw.githubusercontent.com/stephdl/zabbix-postfix-template/master/userparameter_postfix.conf -O /etc/zabbix/zabbix_agentd.d/userparameter_postfix.conf
    OR
    # if you use zabbix_agent2
    wget https://raw.githubusercontent.com/stephdl/zabbix-postfix-template/master/userparameter_postfix.conf -O /etc/zabbix/zabbix_agent2.d/userparameter_postfix.conf

    # create the sudo for zabbix
    cat << 'EOF' > /etc/sudoers.d/40zabbix-agent
    Defaults:zabbix !requiretty
    zabbix ALL=NOPASSWD: /usr/bin/zabbix-postfix-stats.sh
    EOF

The restart zabbix-agent

    systemctl restart zabbix-agent
    or
    systemctl restart zabbix-agent2


Finally import template_app_zabbix.xml and attach it to the server host. Go to : https://raw.githubusercontent.com/stephdl/zabbix-postfix-template/master/template_app_zabbix.xml
do a ctrl+s, save the template to your computer and import it with the zabbix UI (/configuration/Templates/import a template)

For debugging each minute, 2 files are written to /tmp it is the offset of the file and the stats of postfix

    /tmp/zabbix-postfix-offset.dat
    /tmp/postfix_statsfile.dat
