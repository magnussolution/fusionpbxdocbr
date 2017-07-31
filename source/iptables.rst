.. image:: _static/images/logo.png
   :width: 40px
   :alt: Fusionpbx
   :target: https://github.com/fusionpbx/fusionpbx-docs

Basic Rules
~~~~~~~~~~~~

| ``iptables -A INPUT -i lo -j ACCEPT``
| ``iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT``
| ``iptables -A INPUT -p tcp --dport 22 -j ACCEPT``
| ``iptables -A INPUT -p tcp --dport 80 -j ACCEPT``
| ``iptables -A INPUT -p tcp --dport 443 -j ACCEPT``
| ``iptables -A INPUT -p tcp --dport 5060:5069 -j ACCEPT``
| ``iptables -A INPUT -p udp --dport 5060:5069 -j ACCEPT``
| ``iptables -A INPUT -p tcp --dport 5080 -j ACCEPT``
| ``iptables -A INPUT -p udp --dport 5080 -j ACCEPT``
| ``iptables -A INPUT -p udp --dport 16384:32768 -j ACCEPT``
| ``iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT``
| ``iptables -A INPUT -p udp --dport 1194 -j ACCEPT``
| ``iptables -P INPUT DROP``
| ``iptables -P FORWARD DROP``
| ``iptables -P OUTPUT ACCEPT``


Friendly Scanner
~~~~~~~~~~~~~~~~~

Rules to block not so friendly scanner

| ``iptables -I INPUT -j DROP -p tcp --dport 5060 -m string --string "friendly-scanner" --algo bm``
| ``iptables -I INPUT -j DROP -p tcp --dport 5080 -m string --string "friendly-scanner" --algo bm``
| ``iptables -I INPUT -j DROP -p udp --dport 5060 -m string --string "friendly-scanner" --algo bm``
| ``iptables -I INPUT -j DROP -p udp --dport 5080 -m string --string "friendly-scanner" --algo bm``

Show iptable rules
~~~~~~~~~~~~~~~~~~~

| ``sudo iptables -L -v``

Show line numbers
~~~~~~~~~~~~~~~~~~

| ``iptables -L -v --line-numbers``

Delete a line
~~~~~~~~~~~~~~

| Delete line 2
| ``iptables -D INPUT 2``

Flush out iptables
~~~~~~~~~~~~~~~~~~~

| ``iptables -P INPUT ACCEPT``
| ``iptables -P FORWARD ACCEPT``
| ``iptables -P OUTPUT ACCEPT``
| ``iptables -F``


Block IP address
~~~~~~~~~~~~~~~~~

| ``iptables -I INPUT -s 62.210.245.132 -j DROP``

Save Changes
~~~~~~~~~~~~~

Debian & Ubuntu

| ``apt-get install iptables-persistent``
| ``service iptables-persistent save``
|
| ``dpkg-reconfigure iptables-persistent``
