README - Befor Import Templates....

### 1 ### Create SNMPTT ***.conf files.

snmpttconvertmib --in=/usr/share/snmp/mibs/IF-MIB.txt --out=/etc/snmp/IF-MIB.conf.org --debug=2 --net_snmp_perl
snmpttconvertmib --in=/usr/share/snmp/mibs/SNMPv2-MIB.txt --out=/etc/snmp/SNMPv2-MIB.conf.org --debug=2 --net_snmp_perl

cd /etc/snmp/

sed -e "s/^FORMAT\s/FORMAT ZBXTRAP \$aA /g" IF-MIB.conf.org > IF-MIB.conf
sed -e "s/^FORMAT\s/FORMAT ZBXTRAP \$aA /g" SNMPv2-MIB.conf.org > SNMPv2-MIB.conf

### 2 ### Edit snmptt.ini.

vi /etc/snmp/snmptt.ini

 [TrapFiles]
 # A list of snmptt.conf files (this is NOT the snmptrapd.conf file).  The COMPLETE path
 # and filename.  Ex: '/etc/snmp/snmptt.conf'
 snmptt_conf_files = <<END
 /etc/snmp/snmptt.conf
 /etc/snmp/IF-MIB.conf
 /etc/snmp/SNMPv2-MIB.conf
 END

### 3 ### Reload SNMPTT Service.

# service snmptt reload


### 4 ### Add Zabbix Regular expression "snmptrap.other".
@snmptrap.other
1	>>	Normal	 [Character string not included]
2	>>	"LOGONLY"	 [Character string not included]
3	>>	Disaster	 [Character string not included]
4	>>	Critical	 [Character string not included]
5	>>	High	 [Character string not included]
6	>>	Major	 [Character string not included]
7	>>	Average	 [Character string not included]
8	>>	Minor	 [Character string not included]
9	>>	Warning	 [Character string not included]
10	>>	Information	 [Character string not included]


