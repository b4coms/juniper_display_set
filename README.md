# Juniper display set

This script converts standard Juniper config into a list of 'set' commands which you can use 
to configure a Juniper device

Usage
-----
The input is a standard Juniper configuration file like:

```
/* my configuration */


# Conventional SubSystem Config - BR IntSw - cs14l074rs1
# Zone Number: 4
# Model Type: SRX345
# TNCT Version: TNCT_R26.141.00 (ASTRO 2022.X TNCT Application)
# Required Firmware Version: JunOS 20.2X42.3 or 20.2X42.7 or 20.2X42.8 or 20.2X42.10 or 20.2X42.12
# Timestamp: 2024.11.26-10.44.30
# 
# Format: STANZA

groups {
    OSPF-LFA {
        protocols {
            ospf {
                area <*> {
                    interface <*> {
                        node-link-protection;
                    }
                }
            }
        }
    }
    OSPF-BFD {
        protocols {
            ospf {
                area <*> {
                    interface <*> {
                        bfd-liveness-detection {
                            minimum-interval 300;
                            multiplier 3;
                            no-adaptation;
                        }
                    }
                }
            }
        }
    }
    OSPF-INTERFACE {
        protocols {
            ospf {
                area <*> {
                    interface <*> {
                        dead-interval 40;
                        hello-interval 10;
                    }
                }
            }
        }
    }
    PIM-INTERFACE {
        protocols {
            pim {
                interface <*> {
                    mode sparse;
                    hello-interval 5;
                }
            }
        }
    }
    PIM-BFD {
        protocols {
            pim {
                interface <*> {
                    family inet {
                        bfd-liveness-detection {
                            multiplier 3;
                            minimum-interval 300;
                            no-adaptation;
                        }
                    }
                }
            }
        }
    }
    PIM-RP-STATIC {
        protocols {
            pim {
                rp {
                    static {
                        address 10.214.1.227 {
                            version 2;
                            group-ranges {
                                224.0.0.0/4;
                            }
                        }
                        address 10.1.253.73 {
                            version 2;
                            group-ranges {
                                228.4.0.0/19;
                                228.4.64.0/19;
                                228.18.0.0/19;
                                228.18.64.0/19;
                            }
                        }
                        address 10.1.253.81 {
                            version 2;
                            group-ranges {
                                228.4.32.0/19;
                                228.4.96.0/19;
                                228.18.32.0/19;
                                228.18.96.0/19;
                            }
                        }
                        address 10.2.253.73 {
                            version 2;
                            group-ranges {
                                228.8.0.0/19;
                                228.8.64.0/19;
                                228.22.0.0/19;
                                228.22.64.0/19;
                            }
                        }
                        address 10.2.253.81 {
                            version 2;
                            group-ranges {
                                228.8.32.0/19;
                                228.8.96.0/19;
                                228.22.32.0/19;
                                228.22.96.0/19;
                            }
                        }
                        address 10.3.253.73 {
                            version 2;
                            group-ranges {
                                228.12.0.0/19;
                                228.12.64.0/19;
                                228.26.0.0/19;
                                228.26.64.0/19;
                            }
                        }
                        address 10.3.253.81 {
                            version 2;
                            group-ranges {
                                228.12.32.0/19;
                                228.12.96.0/19;
                                228.26.32.0/19;
                                228.26.96.0/19;
                            }
                        }
                        address 10.4.253.73 {
                            version 2;
                            group-ranges {
                                228.16.0.0/19;
                                228.16.64.0/19;
                                228.6.0.0/19;
                                228.6.64.0/19;
                            }
                        }
                        address 10.4.253.81 {
                            version 2;
                            group-ranges {
                                228.16.32.0/19;
                                228.16.96.0/19;
                                228.6.32.0/19;
                                228.6.96.0/19;
                            }
                        }
                        address 10.5.253.73 {
                            version 2;
                            group-ranges {
                                228.20.0.0/19;
                                228.20.64.0/19;
                                228.10.0.0/19;
                                228.10.64.0/19;
                            }
                        }
                        address 10.5.253.81 {
                            version 2;
                            group-ranges {
                                228.20.32.0/19;
                                228.20.96.0/19;
                                228.10.32.0/19;
                                228.10.96.0/19;
                            }
                        }
                        address 10.6.253.73 {
                            version 2;
                            group-ranges {
                                228.24.0.0/19;
                                228.24.64.0/19;
                                228.14.0.0/19;
                                228.14.64.0/19;
                            }
                        }
                        address 10.6.253.81 {
                            version 2;
                            group-ranges {
                                228.24.32.0/19;
                                228.24.96.0/19;
                                228.14.32.0/19;
                                228.14.96.0/19;
                            }
                        }
                        address 10.7.253.73 {
                            version 2;
                            group-ranges {
                                228.28.0.0/19;
                                228.28.64.0/19;
                            }
                        }
                        address 10.7.253.81 {
                            version 2;
                            group-ranges {
                                228.28.32.0/19;
                                228.28.96.0/19;
                            }
                        }
                    }
                }
            }
        }
    }
}




interfaces {
    lo0 {
        unit 0 {
            family inet {
                address 10.214.74.252/32 {
                    primary;
                }
                address 10.214.74.212/32;
                filter {
                    input RE-INPUT;
                }
            }
            family inet6 {
                filter {
                    input RE-INPUT-6;
                }
            }
        }
    }






    ge-0/0/5 {
        speed 100m;
        link-mode full-duplex;
        gigether-options {
            no-auto-negotiation;
        }
        flexible-vlan-tagging;
        native-vlan-id 30;
        unit 30 {
            description "BH";
            vlan-id 30;
            family inet {
                address 192.168.115.62/30;
                mtu 658;
                filter {
                    input BH-INPUT;
                }
            }
        }
    }





    st0 {
        per-unit-scheduler;
        unit 110 {
            family inet {
                address 172.19.0.238/30;
            }
        }
        unit 410 {
            family inet {
                address 172.18.0.238/30;
            }
        }
    }


    irb {
        unit 12 {
            description "LAN";
            family inet {
                targeted-broadcast {
                    forward-only;
                }
                address 10.214.74.254/24;
                filter {
                    input LAN-INT-INPUT-FILTER;
                }
            }
        }
    }
    ge-0/0/0 {
        description Service_PC01;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members USED;
            }
        }
    }
    ge-0/0/1 {
        description GTR8000-100f;
        speed 100m;
        link-mode full-duplex;
        gigether-options {
            no-auto-negotiation;
        }
        ether-options {
            mdi-mode force;
        }
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members USED;
            }
        }
    }
    ge-0/0/2 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/3 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/4 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/6 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/7 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/8 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/9 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/10 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/11 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/12 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/13 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/14 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }
    ge-0/0/15 {
        description OPEN;
        unit 0 {
            family ethernet-switching {
                interface-mode access; vlan members UNUSED;
            }
        }
    }

    ge-0/0/2 disable;
    ge-0/0/3 disable;
    ge-0/0/4 disable;
    ge-0/0/6 disable;
    ge-0/0/7 disable;
    fxp0 disable;
    ge-0/0/8 disable;
    ge-0/0/9 disable;
    ge-0/0/10 disable;
    ge-0/0/11 disable;
    ge-0/0/12 disable;
    ge-0/0/13 disable;
    ge-0/0/14 disable;
    ge-0/0/15 disable;
}

groups {
    rpd_bgp {
        protocols {
            bgp {
                log-updown;
            }
        }
    }
}
apply-groups rpd_bgp;
snmp {
    name cs14l074rs1.convloc74.csub14.zone4;
    location "Zone 4";
    contact "NSWPF"
    v3 {
        usm {
            local-engine {
                user D {
                    authentication-none;
                    privacy-none;
                }
                user M {
                    authentication-none;
                    privacy-none;
                }
                user MotoMaster {
                    authentication-none;
                    privacy-none;
                }
            }
        }
        vacm {
            security-to-group {
                security-model usm {
                    security-name D {
                        group RO;
                    }
                    security-name MotoMaster {
                        group RO;
                    }
                    security-name M {
                        group RW;
                    }
                }
            }
            access {
                group RO {
                    default-context-prefix {
                        security-model usm {

                            security-level none {
                                read-view FULL-VIEW;
                            }
                        }
                    }
                }
                group RW {
                    default-context-prefix {
                        security-model usm {
                            security-level none {
                                read-view FULL-VIEW;
                                write-view FULL-VIEW;
                            }
                        }
                    }
                }
            }
        }
        target-address UEM_MANAGER {
            address 10.4.233.20;
            target-parameters SNMP_V3_PARM;
        }
        target-address UEM_MANAGER_DSR {
            address 10.4.237.20;
            target-parameters SNMP_V3_PARM;
        }
         target-parameters SNMP_V3_PARM {
            parameters {
                message-processing-model v3;
                security-model usm;
                security-level none;
                security-name MotoMaster;
            }
            notify-filter MIB2_OID;
        }
        notify-filter MIB2_OID {
            oid 1.3.6.1 include;
            oid 1.3.111.2.802.1.1.8.0.1 include;
            oid 1.3.6.1.4.1.2636.4.1.9 exclude;
            oid 1.3.6.1.2.1.15.7.2 exclude;
            oid 1.3.6.1.4.1.2636.5.1.1.1.0.2 exclude;
        }
        notify SNMP_V3_TRAP {
            type trap;
        }
    }
    engine-id {
        use-default-ip-address;
    }
    view FULL-VIEW {
        oid .1.3.6.1 include;
    }
    trap-options {
        source-address 10.214.74.252;
    }
    trap-group ALL {
        categories {
            link;
            vrrp-events;
            chassis;
        }
    }
}

system {
    host-name cs14l074rs1;
    time-zone UTC;
    no-redirects;
    no-ping-record-route;
    no-ping-time-stamp;
    arp {
        purging;
    }
    internet-options {
        icmpv4-rate-limit packet-rate 50;
        icmpv6-rate-limit packet-rate 50;
        no-source-quench;
        tcp-drop-synfin-set;
        no-ipv6-path-mtu-discovery;
        no-tcp-reset drop-all-tcp;
    }
    authentication-order radius;
    ports {
        console log-out-on-disconnect;
        auxiliary disable;
    }
    diag-port-authentication {
        encrypted-password "$5$Ve1eDl1m$b.cr06XwT.emyH0Di98y0B7Z03.xCL61uSe1V54CbS8";     }
    root-authentication {
        encrypted-password "$5$Ve1eDl1m$b.cr06XwT.emyH0Di98y0B7Z03.xCL61uSe1V54CbS8";
    }
    radius-server {
        10.4.233.166 {
            port 1812;
            accounting-port 1813;
            secret "$9$Tz6CrlMx-wregJDkTQ0BIEhr";
            source-address 10.214.74.252;
        }
        10.4.237.166 {
            port 1812;
            accounting-port 1813;
            secret "$9$Tz6CrlMx-wregJDkTQ0BIEhr";
            source-address 10.214.74.252;
        }
    }
    login {
        announcement "Csub Router: cs14l074rs1\n";
        message "Use of this device and any related service is your consent to all associated terms, conditions, including consent to monitoring and disclosure provisions.";
        retry-options {
            tries-before-disconnect 3;
            maximum-time 60;
        }
        class super-user-local {
            idle-timeout 10;
            login-alarms;
            permissions all;
        }
        class super-user-remote {
            idle-timeout 300;
            login-alarms;
            permissions all;
        }
        user motorola {
            class super-user-local;
            authentication encrypted-password "$5$iYBXzfmC$JK//3cZvNUYazh4tE847h/1PHyapOodIYac2C7hVp65";
        }
        user super-users    {
            class super-user-remote;
        }
        user readonly-users {
            class read-only;
        }
        password {
            minimum-length 15;
            change-type character-sets;
            minimum-numerics 1;
            minimum-upper-cases 1;
            minimum-lower-cases 1;
            minimum-punctuations 1;
            format sha1;
        }
    }
    services {
        ssh {
            root-login deny;
            no-tcp-forwarding;
            protocol-version v2;
            max-sessions-per-connection 1;
            ciphers [ aes256-ctr aes256-cbc aes192-ctr aes192-cbc aes128-ctr aes128-cbc ];
            macs [ hmac-sha2-512 hmac-sha2-256 hmac-sha1 hmac-sha1-96 ];
            key-exchange [ dh-group14-sha1 group-exchange-sha2 ecdh-sha2-nistp256 ecdh-sha2-nistp384 ecdh-sha2-nistp521 ];
            client-alive-count-max 5;
            client-alive-interval 120;
            connection-limit 10;
            rate-limit 4;
        }
        dhcp-local-server {
            group P2 {
                interface irb.12;
            }
        }
    }
    syslog {
        archive size 5m;
        archive files 3;
        user * {
            any emergency;
            daemon alert;
            change-log info;
        }
        host 10.4.233.249 {
            any info;
            match "!((root) CMD (newsyslog)|/usr/libexec/atrun|(root) CMD (adjkerntz -a)|.*mgd.*auto-snapshot|j-idle-timeout|.*FLOW_MCAST_RPF_FAIL.*|check_configured_tpids)"
            allow-duplicates;
            structured-data;
            source-address 10.214.74.252;
        }
        host 10.4.237.249 {
            any info;
            match "!((root) CMD (newsyslog)|/usr/libexec/atrun|(root) CMD (adjkerntz -a)|.*mgd.*auto-snapshot|j-idle-timeout|.*FLOW_MCAST_RPF_FAIL.*|check_configured_tpids)"
            allow-duplicates;
            structured-data;
            source-address 10.214.74.252;
        }
        file messages {
            any info;
            authorization info;
            daemon info;
            firewall info;
        }
        file audit {
            authorization info;
            interactive-commands info;
        }
        file config-change-log {
            change-log info;
        }
        time-format year;
        source-address 10.214.74.252;
    }
    max-configurations-on-flash 49;
    processes {
        app-engine-management-service disable;
        usb-control disable;
        application-identification disable;
        security-intelligence disable;
        application-security disable;
        advanced-anti-malware disable;
        idp-policy disable;
        utmd disable;
        ppp disable;
        pppoe disable;
        mpls-traceroute disable;
        jsrp-service disable;
    }
    ntp {
        source-address 10.214.74.252;
        boot-server 10.4.233.89;
        server 10.4.233.89 prefer;
        server 10.4.237.89;
    }
}




applications {
    application MAV-Service_s2c {
        protocol tcp source-port 52152-65535 destination-port 591;
    }
    application SYSLOG_TCP {
        term 1_TCP protocol tcp;
    }
    application SYSLOG_TCP {
        term 1_TCP source-port 1025-65535;
    }
    application SYSLOG_TCP {
        term 1_TCP destination-port 514;
    }
    application SYSLOG_TCP {
        term 1_TCP inactivity-timeout 60;
    }
    application MSDP-1 {
        protocol tcp;
    }
    application MSDP-1 {
        destination-port msdp;
    }
    application MSDP-2 {
        protocol tcp;
    }
    application MSDP-2 {
        source-port msdp;
    }
    application-set MSDP {
        application MSDP-1;
    }
    application-set MSDP {
        application MSDP-2;
    }

    application PIM {
        protocol pim;
    }
    application ICMP0 {
        protocol icmp;
    }
    application ICMP0 {
        icmp-type 0;
    }
    application ICMP3 {
        protocol icmp;
    }
    application ICMP3 {
        icmp-type 3;
        icmp-code fragmentation-needed;
    }
    application ICMP8 {
        protocol icmp;
    }
    application ICMP8 {
        icmp-type 8;
    }
    application ICMP11 {
        protocol icmp;
    }
    application ICMP11 {
        icmp-type 11;
    }
    application ICMP12 {
        protocol icmp;
    }
    application ICMP12 {
        icmp-type 12;
    }
    application-set ICMP {
        application ICMP0;
    }
    application-set ICMP {
        application ICMP3;
    }
    application-set ICMP {
        application ICMP8;
    }
    application-set ICMP {
        application ICMP11;
    }
    application-set ICMP {
        application ICMP12;
    }




    application DESU_https_REST {
        protocol tcp source-port 1025-65535;
        protocol tcp destination-port 49600;
    }
    application CTI_MCN_Wave5k {
        protocol udp source-port 49152-65535 destination-port 49392;
    }
    application MAV-Service_https {
        protocol tcp source-port 1025-65535;
        protocol tcp destination-port 49508;
    }
    application OTEK {
        term 1_TCP protocol tcp source-port 49152-65535 destination-port 64416 inactivity-timeout 3600;
    }
    application Aux-Cons {
        protocol tcp source-port 5001 destination-port 50152-65535;
    }
    application Cons-Aux {
        protocol tcp source-port 50152-65535 destination-port 5001;
    }
    application Aux-Comp {
        protocol udp source-port 1054 destination-port 1054;
    }
    application Comp-Aux {
        protocol udp source-port 50152-65535 destination-port 1054;
    }
    application IPIP {
        protocol ipip;
    }
    application IKEin {
        protocol udp source-port 500;
    }
    application IKEout {
        protocol udp destination-port 500;
    }
    application ESP {
        protocol esp;
    }
    application SNMP {
        protocol udp destination-port 161-162;
    }
    application MDLC_over_IP {
        protocol udp destination-port 2002;
    }

}

security {

    screen {
        ids-option SCREEN-1 {
            icmp {
                large;
                ping-death;
                flood threshold 1000;
            }
            ip {
                bad-option;
                source-route-option;
                record-route-option;
                timestamp-option;
                security-option;
                stream-option;
                tear-drop;
                tunnel {
                    ip-in-udp {
                        teredo;
                    }
                }
            }
            tcp {
                land;
                winnuke;
                syn-fin;
                fin-no-ack;
                tcp-no-flag;
                syn-frag;
                port-scan threshold 5000;
                syn-flood;
                tcp-sweep threshold 5000;
            }
            udp {
                port-scan threshold 5000;
            }
            limit-session {
                source-ip-based 5000;
                destination-ip-based 5000;
            }
        }
    }
    zones {
        security-zone ZONE-1 {
            screen SCREEN-1;
        }
    }

    address-book {
        global {
            address 10.214.74.252/32 10.214.74.252/32;





            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.1.233.0/24 10.1.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.2.233.0/24 10.2.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.2.237.0/24 10.2.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.3.233.0/24 10.3.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.3.237.0/24 10.3.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.5.233.0/24 10.5.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.5.237.0/24 10.5.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.6.233.0/24 10.6.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.6.237.0/24 10.6.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.7.233.0/24 10.7.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 145.1.17.0/24 145.1.17.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.0.0.0/24 10.0.0.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.4.233.0/24 10.4.233.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.4.237.0/24 10.4.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.245.128/26 10.4.245.128/26;
            address 10.4.245.128/26 10.4.245.128/26;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.4.245.192/26 10.4.245.192/26;
            address 10.4.245.192/26 10.4.245.192/26;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.1.237.0/24 10.1.237.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.1.245.128/26 10.1.245.128/26;
            address 10.1.245.128/26 10.1.245.128/26;
            address 10.214.74.0/24 10.214.74.0/24;

            address 10.0.0.0/24 10.0.0.0/24;
            address 10.0.1.0/24 10.0.1.0/24;
            address 10.4.224.0/19 10.4.224.0/19;
            address 10.1.224.0/19 10.1.224.0/19;
            address 10.2.224.0/19 10.2.224.0/19;
            address 10.3.224.0/19 10.3.224.0/19;
            address 10.5.224.0/19 10.5.224.0/19;
            address 10.6.224.0/19 10.6.224.0/19;
            address 10.7.224.0/19 10.7.224.0/19;
            address 184.0.0.0/10 184.0.0.0/10;
            address 10.0.0.0/8 10.0.0.0/8;
            address 184.0.0.0/10 184.0.0.0/10;
            address-set ZoneCore {
                address 10.0.0.0/24;
                address 10.0.1.0/24;
                address 10.4.224.0/19;
                address 10.1.224.0/19;
                address 10.2.224.0/19;
                address 10.3.224.0/19;
                address 10.5.224.0/19;
                address 10.6.224.0/19;
                address 10.7.224.0/19;
            }
            address-set AgrSubsite {
                address 184.0.0.0/10;
            }
            address-set AgrSiteSubsite {
                address 10.0.0.0/8;
                address 184.0.0.0/10;
            }
            address 172.19.0.0/20 172.19.0.0/20;
            address 172.18.0.0/20 172.18.0.0/20;
            address 10.214.74.0/24 10.214.74.0/24;
            address 10.214.0.0/16 10.214.0.0/16;
            address 10.214.10.0/24 10.214.10.0/24;
            address 10.214.1.0/24 10.214.1.0/24;
            address 10.214.2.0/24 10.214.2.0/24;
            address-set CWAN {
                address 172.19.0.0/20;
                address 172.18.0.0/20;
            }
            address-set LocalLan {
                address 10.214.74.0/24;
            }
            address-set SumCSite {
                address 10.214.0.0/16;
            }
            address-set ConHubLan {
                address 10.214.10.0/24;
            }
            address-set ConduitHubLan {
                address 10.214.1.0/24;
            }
            address-set CSCHubLan {
                address 10.214.2.0/24;
            }
            address 224.0.0.0/8 224.0.0.0/8;
            address 228.0.0.0/8 228.0.0.0/8;
            address 231.252.0.0/16 231.252.0.0/16;
            address-set Multicast {
                address 224.0.0.0/8;
                address 228.0.0.0/8;
                address 231.252.0.0/16;
            }
            address 172.24.0.0/14 172.24.0.0/14;
            address 10.248.0.0/14 10.248.0.0/14;
            address 183.192.0.0/10 183.192.0.0/10;
            address 172.16.0.0/15 172.16.0.0/15;
            address 172.18.32.0/22 172.18.32.0/22;
            address 172.19.32.0/22 172.19.32.0/22;
            address 172.28.0.0/14 172.28.0.0/14;
            address 10.252.0.0/14 10.252.0.0/14;
            address 172.18.96.0/22 172.18.96.0/22;
            address 172.19.96.0/22 172.19.96.0/22;
            address-set WAN {
                address 172.24.0.0/14;
                address 10.248.0.0/14;
                address 183.192.0.0/10;
                address 172.16.0.0/15;
                address 172.18.32.0/22;
                address 172.19.32.0/22;
                address 172.28.0.0/14;
                address 10.252.0.0/14;
                address 172.18.96.0/22;
                address 172.19.96.0/22;
            }
            address 10.214.1.0/25 10.214.1.0/25;
            address 10.214.1.128/27 10.214.1.128/27;
            address 10.214.2.0/25 10.214.2.0/25;
            address 10.214.2.128/27 10.214.2.128/27;
            address 10.214.3.0/25 10.214.3.0/25;
            address 10.214.3.128/27 10.214.3.128/27;
            address 10.214.4.0/25 10.214.4.0/25;
            address 10.214.4.128/27 10.214.4.128/27;
            address 10.214.5.0/25 10.214.5.0/25;
            address 10.214.5.128/27 10.214.5.128/27;
            address 10.214.6.0/25 10.214.6.0/25;
            address 10.214.6.128/27 10.214.6.128/27;
            address 10.214.7.0/25 10.214.7.0/25;
            address 10.214.7.128/27 10.214.7.128/27;
            address 10.214.8.0/25 10.214.8.0/25;
            address 10.214.8.128/27 10.214.8.128/27;
            address 10.214.9.0/25 10.214.9.0/25;
            address 10.214.9.128/27 10.214.9.128/27;
            address 10.214.10.0/25 10.214.10.0/25;
            address 10.214.10.128/27 10.214.10.128/27;
            address 10.214.11.0/25 10.214.11.0/25;
            address 10.214.11.128/27 10.214.11.128/27;
            address 10.214.12.0/25 10.214.12.0/25;
            address 10.214.12.128/27 10.214.12.128/27;
            address 10.214.13.0/25 10.214.13.0/25;
            address 10.214.13.128/27 10.214.13.128/27;
            address 10.214.14.0/25 10.214.14.0/25;
            address 10.214.14.128/27 10.214.14.128/27;
            address 10.214.15.0/25 10.214.15.0/25;
            address 10.214.15.128/27 10.214.15.128/27;
            address 10.214.16.0/25 10.214.16.0/25;
            address 10.214.16.128/27 10.214.16.128/27;
            address 10.214.17.0/25 10.214.17.0/25;
            address 10.214.17.128/27 10.214.17.128/27;
            address 10.214.31.0/25 10.214.31.0/25;
            address 10.214.31.128/27 10.214.31.128/27;
            address 10.214.32.0/25 10.214.32.0/25;
            address 10.214.32.128/27 10.214.32.128/27;
            address 10.214.33.0/25 10.214.33.0/25;
            address 10.214.33.128/27 10.214.33.128/27;
            address 10.214.34.0/25 10.214.34.0/25;
            address 10.214.34.128/27 10.214.34.128/27;
            address 10.214.35.0/25 10.214.35.0/25;
            address 10.214.35.128/27 10.214.35.128/27;
            address 10.214.36.0/25 10.214.36.0/25;
            address 10.214.36.128/27 10.214.36.128/27;
            address 10.214.37.0/25 10.214.37.0/25;
            address 10.214.37.128/27 10.214.37.128/27;
            address 10.214.38.0/25 10.214.38.0/25;
            address 10.214.38.128/27 10.214.38.128/27;
            address 10.214.39.0/25 10.214.39.0/25;
            address 10.214.39.128/27 10.214.39.128/27;
            address 10.214.40.0/25 10.214.40.0/25;
            address 10.214.40.128/27 10.214.40.128/27;
            address 10.214.41.0/25 10.214.41.0/25;
            address 10.214.41.128/27 10.214.41.128/27;
            address 10.214.42.0/25 10.214.42.0/25;
            address 10.214.42.128/27 10.214.42.128/27;
            address 10.214.43.0/25 10.214.43.0/25;
            address 10.214.43.128/27 10.214.43.128/27;
            address 10.214.44.0/25 10.214.44.0/25;
            address 10.214.44.128/27 10.214.44.128/27;
            address 10.214.45.0/25 10.214.45.0/25;
            address 10.214.45.128/27 10.214.45.128/27;
            address 10.214.46.0/25 10.214.46.0/25;
            address 10.214.46.128/27 10.214.46.128/27;
            address 10.214.47.0/25 10.214.47.0/25;
            address 10.214.47.128/27 10.214.47.128/27;
            address 10.214.48.0/25 10.214.48.0/25;
            address 10.214.48.128/27 10.214.48.128/27;
            address 10.214.49.0/25 10.214.49.0/25;
            address 10.214.49.128/27 10.214.49.128/27;
            address 10.214.50.0/25 10.214.50.0/25;
            address 10.214.50.128/27 10.214.50.128/27;
            address 10.214.51.0/25 10.214.51.0/25;
            address 10.214.51.128/27 10.214.51.128/27;
            address 10.214.52.0/25 10.214.52.0/25;
            address 10.214.52.128/27 10.214.52.128/27;
            address 10.214.53.0/25 10.214.53.0/25;
            address 10.214.53.128/27 10.214.53.128/27;
            address 10.214.54.0/25 10.214.54.0/25;
            address 10.214.54.128/27 10.214.54.128/27;
            address 10.214.55.0/25 10.214.55.0/25;
            address 10.214.55.128/27 10.214.55.128/27;
            address 10.214.56.0/25 10.214.56.0/25;
            address 10.214.56.128/27 10.214.56.128/27;
            address 10.214.57.0/25 10.214.57.0/25;
            address 10.214.57.128/27 10.214.57.128/27;
            address 10.214.58.0/25 10.214.58.0/25;
            address 10.214.58.128/27 10.214.58.128/27;
            address 10.214.59.0/25 10.214.59.0/25;
            address 10.214.59.128/27 10.214.59.128/27;
            address 10.214.60.0/25 10.214.60.0/25;
            address 10.214.60.128/27 10.214.60.128/27;
            address 10.214.61.0/25 10.214.61.0/25;
            address 10.214.61.128/27 10.214.61.128/27;
            address 10.214.62.0/25 10.214.62.0/25;
            address 10.214.62.128/27 10.214.62.128/27;
            address 10.214.63.0/25 10.214.63.0/25;
            address 10.214.63.128/27 10.214.63.128/27;
            address 10.214.64.0/25 10.214.64.0/25;
            address 10.214.64.128/27 10.214.64.128/27;
            address 10.214.65.0/25 10.214.65.0/25;
            address 10.214.65.128/27 10.214.65.128/27;
            address 10.214.66.0/25 10.214.66.0/25;
            address 10.214.66.128/27 10.214.66.128/27;
            address 10.214.67.0/25 10.214.67.0/25;
            address 10.214.67.128/27 10.214.67.128/27;
            address 10.214.68.0/25 10.214.68.0/25;
            address 10.214.68.128/27 10.214.68.128/27;
            address 10.214.69.0/25 10.214.69.0/25;
            address 10.214.69.128/27 10.214.69.128/27;
            address 10.214.70.0/25 10.214.70.0/25;
            address 10.214.70.128/27 10.214.70.128/27;
            address 10.214.71.0/25 10.214.71.0/25;
            address 10.214.71.128/27 10.214.71.128/27;
            address 10.214.72.0/25 10.214.72.0/25;
            address 10.214.72.128/27 10.214.72.128/27;
            address 10.214.73.0/25 10.214.73.0/25;
            address 10.214.73.128/27 10.214.73.128/27;
            address 10.214.74.0/25 10.214.74.0/25;
            address 10.214.74.128/27 10.214.74.128/27;
            address 10.214.75.0/25 10.214.75.0/25;
            address 10.214.75.128/27 10.214.75.128/27;
            address 10.214.76.0/25 10.214.76.0/25;
            address 10.214.76.128/27 10.214.76.128/27;
            address 10.214.77.0/25 10.214.77.0/25;
            address 10.214.77.128/27 10.214.77.128/27;
            address 10.214.78.0/25 10.214.78.0/25;
            address 10.214.78.128/27 10.214.78.128/27;
            address 10.214.79.0/25 10.214.79.0/25;
            address 10.214.79.128/27 10.214.79.128/27;
            address 10.214.80.0/25 10.214.80.0/25;
            address 10.214.80.128/27 10.214.80.128/27;
            address 10.214.81.0/25 10.214.81.0/25;
            address 10.214.81.128/27 10.214.81.128/27;
            address 10.214.82.0/25 10.214.82.0/25;
            address 10.214.82.128/27 10.214.82.128/27;
            address 10.214.83.0/25 10.214.83.0/25;
            address 10.214.83.128/27 10.214.83.128/27;
            address 10.214.84.0/25 10.214.84.0/25;
            address 10.214.84.128/27 10.214.84.128/27;
            address 10.214.85.0/25 10.214.85.0/25;
            address 10.214.85.128/27 10.214.85.128/27;
            address 10.214.86.0/25 10.214.86.0/25;
            address 10.214.86.128/27 10.214.86.128/27;
            address 10.214.87.0/25 10.214.87.0/25;
            address 10.214.87.128/27 10.214.87.128/27;
            address 10.214.88.0/25 10.214.88.0/25;
            address 10.214.88.128/27 10.214.88.128/27;
            address 10.214.89.0/25 10.214.89.0/25;
            address 10.214.89.128/27 10.214.89.128/27;
            address 10.214.90.0/25 10.214.90.0/25;
            address 10.214.90.128/27 10.214.90.128/27;
            address 10.214.91.0/25 10.214.91.0/25;
            address 10.214.91.128/27 10.214.91.128/27;
            address 10.214.92.0/25 10.214.92.0/25;
            address 10.214.92.128/27 10.214.92.128/27;
            address 10.214.93.0/25 10.214.93.0/25;
            address 10.214.93.128/27 10.214.93.128/27;
            address 10.214.94.0/25 10.214.94.0/25;
            address 10.214.94.128/27 10.214.94.128/27;
            address 10.214.95.0/25 10.214.95.0/25;
            address 10.214.95.128/27 10.214.95.128/27;
            address 10.214.96.0/25 10.214.96.0/25;
            address 10.214.96.128/27 10.214.96.128/27;
            address 10.214.97.0/25 10.214.97.0/25;
            address 10.214.97.128/27 10.214.97.128/27;
            address 10.214.98.0/25 10.214.98.0/25;
            address 10.214.98.128/27 10.214.98.128/27;
            address 10.214.99.0/25 10.214.99.0/25;
            address 10.214.99.128/27 10.214.99.128/27;
            address 10.214.100.0/25 10.214.100.0/25;
            address 10.214.100.128/27 10.214.100.128/27;
            address 10.214.101.0/25 10.214.101.0/25;
            address 10.214.101.128/27 10.214.101.128/27;
            address 10.214.102.0/25 10.214.102.0/25;
            address 10.214.102.128/27 10.214.102.128/27;
            address 10.214.103.0/25 10.214.103.0/25;
            address 10.214.103.128/27 10.214.103.128/27;
            address 10.214.104.0/25 10.214.104.0/25;
            address 10.214.104.128/27 10.214.104.128/27;
            address 10.214.105.0/25 10.214.105.0/25;
            address 10.214.105.128/27 10.214.105.128/27;
            address 10.214.106.0/25 10.214.106.0/25;
            address 10.214.106.128/27 10.214.106.128/27;
            address 10.214.107.0/25 10.214.107.0/25;
            address 10.214.107.128/27 10.214.107.128/27;
            address 10.214.108.0/25 10.214.108.0/25;
            address 10.214.108.128/27 10.214.108.128/27;
            address 10.214.109.0/25 10.214.109.0/25;
            address 10.214.109.128/27 10.214.109.128/27;
            address 10.214.110.0/25 10.214.110.0/25;
            address 10.214.110.128/27 10.214.110.128/27;
            address 10.214.111.0/25 10.214.111.0/25;
            address 10.214.111.128/27 10.214.111.128/27;
            address 10.214.112.0/25 10.214.112.0/25;
            address 10.214.112.128/27 10.214.112.128/27;
            address 10.214.113.0/25 10.214.113.0/25;
            address 10.214.113.128/27 10.214.113.128/27;
            address 10.214.114.0/25 10.214.114.0/25;
            address 10.214.114.128/27 10.214.114.128/27;
            address 10.214.115.0/25 10.214.115.0/25;
            address 10.214.115.128/27 10.214.115.128/27;
            address 10.214.116.0/25 10.214.116.0/25;
            address 10.214.116.128/27 10.214.116.128/27;
            address 10.214.117.0/25 10.214.117.0/25;
            address 10.214.117.128/27 10.214.117.128/27;
            address 10.214.118.0/25 10.214.118.0/25;
            address 10.214.118.128/27 10.214.118.128/27;
            address 10.214.119.0/25 10.214.119.0/25;
            address 10.214.119.128/27 10.214.119.128/27;
            address 10.214.120.0/25 10.214.120.0/25;
            address 10.214.120.128/27 10.214.120.128/27;
            address 10.214.121.0/25 10.214.121.0/25;
            address 10.214.121.128/27 10.214.121.128/27;
            address 10.214.122.0/25 10.214.122.0/25;
            address 10.214.122.128/27 10.214.122.128/27;
            address 10.214.123.0/25 10.214.123.0/25;
            address 10.214.123.128/27 10.214.123.128/27;
            address 10.214.124.0/25 10.214.124.0/25;
            address 10.214.124.128/27 10.214.124.128/27;
            address 10.214.125.0/25 10.214.125.0/25;
            address 10.214.125.128/27 10.214.125.128/27;
            address 10.214.126.0/25 10.214.126.0/25;
            address 10.214.126.128/27 10.214.126.128/27;
            address 10.214.127.0/25 10.214.127.0/25;
            address 10.214.127.128/27 10.214.127.128/27;
            address 10.214.128.0/25 10.214.128.0/25;
            address 10.214.128.128/27 10.214.128.128/27;
            address 10.214.129.0/25 10.214.129.0/25;
            address 10.214.129.128/27 10.214.129.128/27;
            address-set distConvDynamicPool {
                address 10.214.1.0/25;
                address 10.214.1.128/27;
                address 10.214.2.0/25;
                address 10.214.2.128/27;
                address 10.214.3.0/25;
                address 10.214.3.128/27;
                address 10.214.4.0/25;
                address 10.214.4.128/27;
                address 10.214.5.0/25;
                address 10.214.5.128/27;
                address 10.214.6.0/25;
                address 10.214.6.128/27;
                address 10.214.7.0/25;
                address 10.214.7.128/27;
                address 10.214.8.0/25;
                address 10.214.8.128/27;
                address 10.214.9.0/25;
                address 10.214.9.128/27;
                address 10.214.10.0/25;
                address 10.214.10.128/27;
                address 10.214.11.0/25;
                address 10.214.11.128/27;
                address 10.214.12.0/25;
                address 10.214.12.128/27;
                address 10.214.13.0/25;
                address 10.214.13.128/27;
                address 10.214.14.0/25;
                address 10.214.14.128/27;
                address 10.214.15.0/25;
                address 10.214.15.128/27;
                address 10.214.16.0/25;
                address 10.214.16.128/27;
                address 10.214.17.0/25;
                address 10.214.17.128/27;
                address 10.214.31.0/25;
                address 10.214.31.128/27;
                address 10.214.32.0/25;
                address 10.214.32.128/27;
                address 10.214.33.0/25;
                address 10.214.33.128/27;
                address 10.214.34.0/25;
                address 10.214.34.128/27;
                address 10.214.35.0/25;
                address 10.214.35.128/27;
                address 10.214.36.0/25;
                address 10.214.36.128/27;
                address 10.214.37.0/25;
                address 10.214.37.128/27;
                address 10.214.38.0/25;
                address 10.214.38.128/27;
                address 10.214.39.0/25;
                address 10.214.39.128/27;
                address 10.214.40.0/25;
                address 10.214.40.128/27;
                address 10.214.41.0/25;
                address 10.214.41.128/27;
                address 10.214.42.0/25;
                address 10.214.42.128/27;
                address 10.214.43.0/25;
                address 10.214.43.128/27;
                address 10.214.44.0/25;
                address 10.214.44.128/27;
                address 10.214.45.0/25;
                address 10.214.45.128/27;
                address 10.214.46.0/25;
                address 10.214.46.128/27;
                address 10.214.47.0/25;
                address 10.214.47.128/27;
                address 10.214.48.0/25;
                address 10.214.48.128/27;
                address 10.214.49.0/25;
                address 10.214.49.128/27;
                address 10.214.50.0/25;
                address 10.214.50.128/27;
                address 10.214.51.0/25;
                address 10.214.51.128/27;
                address 10.214.52.0/25;
                address 10.214.52.128/27;
                address 10.214.53.0/25;
                address 10.214.53.128/27;
                address 10.214.54.0/25;
                address 10.214.54.128/27;
                address 10.214.55.0/25;
                address 10.214.55.128/27;
                address 10.214.56.0/25;
                address 10.214.56.128/27;
                address 10.214.57.0/25;
                address 10.214.57.128/27;
                address 10.214.58.0/25;
                address 10.214.58.128/27;
                address 10.214.59.0/25;
                address 10.214.59.128/27;
                address 10.214.60.0/25;
                address 10.214.60.128/27;
                address 10.214.61.0/25;
                address 10.214.61.128/27;
                address 10.214.62.0/25;
                address 10.214.62.128/27;
                address 10.214.63.0/25;
                address 10.214.63.128/27;
                address 10.214.64.0/25;
                address 10.214.64.128/27;
                address 10.214.65.0/25;
                address 10.214.65.128/27;
                address 10.214.66.0/25;
                address 10.214.66.128/27;
                address 10.214.67.0/25;
                address 10.214.67.128/27;
                address 10.214.68.0/25;
                address 10.214.68.128/27;
                address 10.214.69.0/25;
                address 10.214.69.128/27;
                address 10.214.70.0/25;
                address 10.214.70.128/27;
                address 10.214.71.0/25;
                address 10.214.71.128/27;
                address 10.214.72.0/25;
                address 10.214.72.128/27;
                address 10.214.73.0/25;
                address 10.214.73.128/27;
                address 10.214.74.0/25;
                address 10.214.74.128/27;
                address 10.214.75.0/25;
                address 10.214.75.128/27;
                address 10.214.76.0/25;
                address 10.214.76.128/27;
                address 10.214.77.0/25;
                address 10.214.77.128/27;
                address 10.214.78.0/25;
                address 10.214.78.128/27;
                address 10.214.79.0/25;
                address 10.214.79.128/27;
                address 10.214.80.0/25;
                address 10.214.80.128/27;
                address 10.214.81.0/25;
                address 10.214.81.128/27;
                address 10.214.82.0/25;
                address 10.214.82.128/27;
                address 10.214.83.0/25;
                address 10.214.83.128/27;
                address 10.214.84.0/25;
                address 10.214.84.128/27;
                address 10.214.85.0/25;
                address 10.214.85.128/27;
                address 10.214.86.0/25;
                address 10.214.86.128/27;
                address 10.214.87.0/25;
                address 10.214.87.128/27;
                address 10.214.88.0/25;
                address 10.214.88.128/27;
                address 10.214.89.0/25;
                address 10.214.89.128/27;
                address 10.214.90.0/25;
                address 10.214.90.128/27;
                address 10.214.91.0/25;
                address 10.214.91.128/27;
                address 10.214.92.0/25;
                address 10.214.92.128/27;
                address 10.214.93.0/25;
                address 10.214.93.128/27;
                address 10.214.94.0/25;
                address 10.214.94.128/27;
                address 10.214.95.0/25;
                address 10.214.95.128/27;
                address 10.214.96.0/25;
                address 10.214.96.128/27;
                address 10.214.97.0/25;
                address 10.214.97.128/27;
                address 10.214.98.0/25;
                address 10.214.98.128/27;
                address 10.214.99.0/25;
                address 10.214.99.128/27;
                address 10.214.100.0/25;
                address 10.214.100.128/27;
                address 10.214.101.0/25;
                address 10.214.101.128/27;
                address 10.214.102.0/25;
                address 10.214.102.128/27;
                address 10.214.103.0/25;
                address 10.214.103.128/27;
                address 10.214.104.0/25;
                address 10.214.104.128/27;
                address 10.214.105.0/25;
                address 10.214.105.128/27;
                address 10.214.106.0/25;
                address 10.214.106.128/27;
                address 10.214.107.0/25;
                address 10.214.107.128/27;
                address 10.214.108.0/25;
                address 10.214.108.128/27;
                address 10.214.109.0/25;
                address 10.214.109.128/27;
                address 10.214.110.0/25;
                address 10.214.110.128/27;
                address 10.214.111.0/25;
                address 10.214.111.128/27;
                address 10.214.112.0/25;
                address 10.214.112.128/27;
                address 10.214.113.0/25;
                address 10.214.113.128/27;
                address 10.214.114.0/25;
                address 10.214.114.128/27;
                address 10.214.115.0/25;
                address 10.214.115.128/27;
                address 10.214.116.0/25;
                address 10.214.116.128/27;
                address 10.214.117.0/25;
                address 10.214.117.128/27;
                address 10.214.118.0/25;
                address 10.214.118.128/27;
                address 10.214.119.0/25;
                address 10.214.119.128/27;
                address 10.214.120.0/25;
                address 10.214.120.128/27;
                address 10.214.121.0/25;
                address 10.214.121.128/27;
                address 10.214.122.0/25;
                address 10.214.122.128/27;
                address 10.214.123.0/25;
                address 10.214.123.128/27;
                address 10.214.124.0/25;
                address 10.214.124.128/27;
                address 10.214.125.0/25;
                address 10.214.125.128/27;
                address 10.214.126.0/25;
                address 10.214.126.128/27;
                address 10.214.127.0/25;
                address 10.214.127.128/27;
                address 10.214.128.0/25;
                address 10.214.128.128/27;
                address 10.214.129.0/25;
                address 10.214.129.128/27;
            }
            address 10.51.1.100/32 10.51.1.100/32;
            address 10.53.1.1/32 10.53.1.1/32;
            address-set KMF_NAT_CEN1 {
                address 10.51.1.100/32;
            }
            address-set KMF_NAT_CEN5 {
                address 10.53.1.1/32;
            }
            address 145.1.17.0/24 145.1.17.0/24;
            address-set SSC {
                address 145.1.17.0/24;
            }
        }
    }

    policies {
        from-zone ZONE-1 to-zone ZONE-1 {
            policy SYSLOG_TCP_fix {
                match {
                    source-address any;
                    destination-address any;
                    application SYSLOG_TCP;
                }
                then {
                    permit;
                }
            }
            policy OTEK_fix {
                match {
                    source-address any;
                    destination-address any;
                    application OTEK;
                }
                then {
                    permit;
                }
            }
            policy MSDP-POLICY {
                match {
                    source-address any;
                    destination-address any;
                    application MSDP;
                }
                then {
                    permit;
                }
            }
            policy WAN-to-WAN {
                match {
                    source-address LocalLan;
                    source-address-excluded;
                    destination-address LocalLan;
                    destination-address-excluded;
                    application any;
                }
                then {
                    permit;
                }
            }
        }
        from-zone ZONE-1 to-zone junos-host {
            policy SELF-TRAFFIC-1 {
                match {
                    source-address any;
                    destination-address any;
                    application any;
                }
                then {
                    permit;
                }
            }
        }
        from-zone junos-host to-zone ZONE-1 {
            policy SELF-TRAFFIC-2 {
                match {
                    source-address any;
                    destination-address any;
                    application any;
                }
                then {
                    permit;
                }
            }
        }
        global {
            policy TFTP {
                match { source-address 10.214.74.0/24 destination-address 10.4.233.0/24 application junos-tftp }
                match { source-address 10.4.233.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.4.237.0/24 application junos-tftp }
                match { source-address 10.4.237.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.1.233.0/24 application junos-tftp }
                match { source-address 10.1.233.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.1.237.0/24 application junos-tftp }
                match { source-address 10.1.237.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.2.233.0/24 application junos-tftp }
                match { source-address 10.2.233.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.2.237.0/24 application junos-tftp }
                match { source-address 10.2.237.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.3.233.0/24 application junos-tftp }
                match { source-address 10.3.233.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.3.237.0/24 application junos-tftp }
                match { source-address 10.3.237.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.5.233.0/24 application junos-tftp }
                match { source-address 10.5.233.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.5.237.0/24 application junos-tftp }
                match { source-address 10.5.237.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.6.233.0/24 application junos-tftp }
                match { source-address 10.6.233.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.6.237.0/24 application junos-tftp }
                match { source-address 10.6.237.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.7.233.0/24 application junos-tftp }
                match { source-address 10.7.233.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 145.1.17.0/24 application junos-tftp }
                match { source-address 145.1.17.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.0.0.0/24 application junos-tftp }
                match { source-address 10.0.0.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.0.1.0/24 application junos-tftp }
                match { source-address 10.0.1.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.214.1.0/24 application junos-tftp }
                match { source-address 10.214.1.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.214.2.0/24 application junos-tftp }
                match { source-address 10.214.2.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.10.0/24 destination-address 10.214.74.0/24 application junos-tftp }
                match { source-address 10.214.74.0/24 destination-address 10.214.10.0/24 application junos-tftp }
                then {
                    permit;
                }
            }
            policy SNMP {
                match { source-address 10.214.74.0/24 destination-address 10.4.233.0/24 application SNMP }
                match { source-address 10.4.233.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.4.237.0/24 application SNMP }
                match { source-address 10.4.237.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.1.233.0/24 application SNMP }
                match { source-address 10.1.233.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.1.237.0/24 application SNMP }
                match { source-address 10.1.237.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.2.233.0/24 application SNMP }
                match { source-address 10.2.233.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.2.237.0/24 application SNMP }
                match { source-address 10.2.237.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.3.233.0/24 application SNMP }
                match { source-address 10.3.233.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.3.237.0/24 application SNMP }
                match { source-address 10.3.237.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.5.233.0/24 application SNMP }
                match { source-address 10.5.233.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.5.237.0/24 application SNMP }
                match { source-address 10.5.237.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.6.233.0/24 application SNMP }
                match { source-address 10.6.233.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.6.237.0/24 application SNMP }
                match { source-address 10.6.237.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.7.233.0/24 application SNMP }
                match { source-address 10.7.233.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 145.1.17.0/24 application SNMP }
                match { source-address 145.1.17.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.0.0.0/24 application SNMP }
                match { source-address 10.0.0.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.0.1.0/24 application SNMP }
                match { source-address 10.0.1.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.214.1.0/24 application SNMP }
                match { source-address 10.214.1.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.214.2.0/24 application SNMP }
                match { source-address 10.214.2.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.10.0/24 destination-address 10.214.74.0/24 application SNMP }
                match { source-address 10.214.74.0/24 destination-address 10.214.10.0/24 application SNMP }
                then {
                    permit;
                }
            }
            policy SSH-TELNET {
                match { source-address 10.214.74.0/24 destination-address 10.4.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.4.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.4.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.4.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.1.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.1.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.1.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.1.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.2.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.2.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.2.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.2.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.3.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.3.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.3.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.3.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.5.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.5.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.5.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.5.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.6.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.6.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.6.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.6.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.7.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.7.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 145.1.17.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 145.1.17.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.0.0.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.0.0.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.0.1.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.0.1.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.1.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.1.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.2.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.2.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.10.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.10.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.4.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.4.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.4.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.4.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.1.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.1.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.1.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.1.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.2.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.2.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.2.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.2.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.3.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.3.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.3.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.3.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.5.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.5.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.5.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.5.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.6.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.6.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.6.237.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.6.237.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.7.233.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.7.233.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 145.1.17.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 145.1.17.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.0.0.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.0.0.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.0.1.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.0.1.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.1.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.1.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.2.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.2.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.10.0/24 destination-address 10.214.74.0/24 application [ junos-ssh junos-telnet ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.10.0/24 application [ junos-ssh junos-telnet ] }
                then {
                    permit {
                        tcp-options {
                            syn-check-required;
                            sequence-check-required;
                        }
                    }
                }
            }
            policy HTTP {
                match { source-address 10.214.74.0/24 destination-address 10.4.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.4.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.4.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.4.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.1.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.1.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.1.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.1.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.2.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.2.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.2.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.2.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.3.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.3.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.3.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.3.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.5.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.5.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.5.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.5.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.6.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.6.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.6.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.6.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.7.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.7.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 145.1.17.0/24 application [ junos-http junos-https ] }
                match { source-address 145.1.17.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.0.0.0/24 application [ junos-http junos-https ] }
                match { source-address 10.0.0.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.0.1.0/24 application [ junos-http junos-https ] }
                match { source-address 10.0.1.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.1.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.1.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.2.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.2.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.10.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.10.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.4.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.4.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.4.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.4.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.1.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.1.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.1.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.1.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.2.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.2.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.2.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.2.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.3.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.3.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.3.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.3.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.5.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.5.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.5.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.5.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.6.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.6.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.6.237.0/24 application [ junos-http junos-https ] }
                match { source-address 10.6.237.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.7.233.0/24 application [ junos-http junos-https ] }
                match { source-address 10.7.233.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 145.1.17.0/24 application [ junos-http junos-https ] }
                match { source-address 145.1.17.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.0.0.0/24 application [ junos-http junos-https ] }
                match { source-address 10.0.0.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.0.1.0/24 application [ junos-http junos-https ] }
                match { source-address 10.0.1.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.1.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.1.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.2.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.2.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.10.0/24 destination-address 10.214.74.0/24 application [ junos-http junos-https ] }
                match { source-address 10.214.74.0/24 destination-address 10.214.10.0/24 application [ junos-http junos-https ] }
                then {
                    permit {
                        tcp-options {
                            syn-check-required;
                            sequence-check-required;
                        }
                    }
                }
            }
            policy SYSLOG {
                match { source-address 10.214.74.0/24 destination-address 10.4.233.0/24 application junos-syslog }
                match { source-address 10.4.233.0/24 destination-address 10.214.74.0/24 application junos-syslog }
                match { source-address 10.214.74.0/24 destination-address 10.4.237.0/24 application junos-syslog }
                match { source-address 10.4.237.0/24 destination-address 10.214.74.0/24 application junos-syslog }
                match { source-address 10.214.74.0/24 destination-address 10.4.245.128/26 application junos-syslog }
                match { source-address 10.4.245.128/26 destination-address 10.214.74.0/24 application junos-syslog }
                match { source-address 10.214.74.0/24 destination-address 10.4.245.192/26 application junos-syslog }
                match { source-address 10.4.245.192/26 destination-address 10.214.74.0/24 application junos-syslog }
                match { source-address 10.214.74.0/24 destination-address 10.1.237.0/24 application junos-syslog }
                match { source-address 10.1.237.0/24 destination-address 10.214.74.0/24 application junos-syslog }
                match { source-address 10.214.74.0/24 destination-address 10.1.245.128/26 application junos-syslog }
                match { source-address 10.1.245.128/26 destination-address 10.214.74.0/24 application junos-syslog }
                then { permit }
            }






            policy NONSTANDARD-1 { match { source-address any destination-address Multicast application any }}
            policy NONSTANDARD-2 { match { source-address any destination-address any application PIM }}
            policy NONSTANDARD-3 { match { source-address LocalLan destination-address ZoneCore application any }}
            policy NONSTANDARD-3 { match { source-address LocalLan destination-address ConHubLan application any }}
            policy NONSTANDARD-3 { match { source-address LocalLan destination-address ConduitHubLan application any }}
            policy NONSTANDARD-3 { match { source-address LocalLan destination-address CSCHubLan application any }}
            policy NONSTANDARD-3 { match { source-address LocalLan destination-address LocalLan application any }}
            policy NONSTANDARD-4 { match { source-address LocalLan destination-address SSC application any }}
            policy NONSTANDARD-5 { match { source-address LocalLan destination-address AgrSiteSubsite application Aux-Cons }}
 
            policy NONSTANDARD-6 { match { source-address any destination-address Multicast application any }}
            policy NONSTANDARD-7 { match { source-address any destination-address any application PIM }}
            policy NONSTANDARD-8 { match { source-address any destination-address LocalLan application ICMP }}
            policy NONSTANDARD-9 { match { source-address CWAN destination-address CWAN application any }}
            policy NONSTANDARD-10 { match { source-address ZoneCore destination-address LocalLan application any }}
            policy NONSTANDARD-10 { match { source-address ConHubLan destination-address LocalLan application any }}
            policy NONSTANDARD-10 { match { source-address ConduitHubLan destination-address LocalLan application any }}
            policy NONSTANDARD-10 { match { source-address CSCHubLan destination-address LocalLan application any }}
            policy NONSTANDARD-11 { match { source-address AgrSiteSubsite destination-address LocalLan application Cons-Aux }}
            policy NONSTANDARD-12 { match { source-address SSC destination-address LocalLan application any }}


            policy NONSTANDARD-1 { then { permit }}
            policy NONSTANDARD-1 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-1 { then { permit { tcp-options { syn-check-required }}}}
            policy NONSTANDARD-2 { then { permit }}
            policy NONSTANDARD-2 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-2 { then { permit { tcp-options { syn-check-required }}}}
            policy NONSTANDARD-3 { then { permit }}
            policy NONSTANDARD-3 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-3 { then { permit { tcp-options { syn-check-required }}}}
            policy NONSTANDARD-4 { then { permit }}
            policy NONSTANDARD-4 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-4 { then { permit { tcp-options { syn-check-required }}}}
            policy NONSTANDARD-5 { then { permit }}
            policy NONSTANDARD-5 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-5 { then { permit { tcp-options { syn-check-required }}}}
            policy NONSTANDARD-6 { then { permit }}
            policy NONSTANDARD-6 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-6 { then { permit { tcp-options { syn-check-required }}}}
            policy NONSTANDARD-7 { then { permit }}
            policy NONSTANDARD-7 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-7 { then { permit { tcp-options { syn-check-required }}}}
            policy NONSTANDARD-8 { then { permit }}
            policy NONSTANDARD-8 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-8 { then { permit { tcp-options { syn-check-required }}}}
            policy NONSTANDARD-9 { then { permit }}
            policy NONSTANDARD-9 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-9 { then { permit { tcp-options { syn-check-required }}}}
            policy NONSTANDARD-10 { then { permit }}
            policy NONSTANDARD-10 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-10 { then { permit { tcp-options { syn-check-required }}}}
            policy NONSTANDARD-11 { then { permit }}
            policy NONSTANDARD-11 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-11 { then { permit { tcp-options { syn-check-required }}}}
            policy NONSTANDARD-12 { then { permit }}
            policy NONSTANDARD-12 { then { permit { tcp-options { sequence-check-required }}}}
            policy NONSTANDARD-12 { then { permit { tcp-options { syn-check-required }}}}
            policy ZoneCore_to_HubLan {
                match {
                    source-address ZoneCore;
                    destination-address ConduitHubLan;
                    destination-address CSCHubLan;
                    application DESU_https_REST;
                }
                then {
                    permit;
                }
            }
            policy CSUB_to_CSMS {
                match {
                    source-address ConduitHubLan;
                    source-address CSCHubLan;
                    destination-address ZoneCore;
                    application MAV-Service_https;
                }
                then {
                    permit;
                }
            }
            policy CSUB_to_KMF {
                match {
                    source-address distConvDynamicPool;
                    destination-address [ KMF_NAT_CEN1 KMF_NAT_CEN5];
                    application OTEK;
                }
                then {
                    permit;
                }
            }
             policy MDLC_over_IP {
                match {
                    source-address any;
                    destination-address any;
                    application MDLC_over_IP;
                }
                then {
                    permit;
                }
            }
        }
    }

}
security {
    log {
        mode stream;
        source-address 10.214.74.252;
        stream SECURITYLOG {
            format syslog;
            host {
                10.4.233.249;
            }
            rate-limit {
                1000;
            }
        }
    }
    policies {
        policy-rematch extensive;
        default-policy {
            deny-all;
        }
    }
}
security {
    ike {
        proposal IKE-PROP {
            authentication-method pre-shared-keys;
            dh-group group20;
            authentication-algorithm sha-384;
            encryption-algorithm aes-256-cbc;
            lifetime-seconds 28800;
        }
        policy IKE-POL {
            mode main;
            proposals IKE-PROP;
            pre-shared-key ascii-text "$9$zjGU39pKvL-b2KMaUHmF31RhSyK";
        }
        policy IKE-POL-110 {
            mode main;
            proposals IKE-PROP;
            pre-shared-key ascii-text "$9$zjGU39pKvL-b2KMaUHmF31RhSyK";
        }
        gateway IKE-GW-110 {
            ike-policy IKE-POL-110;
            address 192.168.115.50;
            local-address 192.168.115.62;
            external-interface ge-0/0/5.30;
            version v2-only;
        }
        policy IKE-POL-410 {
            mode main;
            proposals IKE-PROP;
            pre-shared-key ascii-text "$9$zjGU39pKvL-b2KMaUHmF31RhSyK";
        }
        gateway IKE-GW-410 {
            ike-policy IKE-POL-410;
            address 192.168.115.51;
            local-address 192.168.115.62;
            external-interface ge-0/0/5.30;
            version v2-only;
        }
    }
    ipsec {
        proposal IPSEC-PROP {
            protocol esp;
            authentication-algorithm hmac-sha-256-128;
            encryption-algorithm aes-256-cbc;
            lifetime-seconds 28800;
        }
        policy IPSEC-POL {
            perfect-forward-secrecy keys group14;
            proposals IPSEC-PROP;
        }
        vpn IPSEC-VPN-110 {
            ike {
                ipsec-policy IPSEC-POL;
                gateway IKE-GW-110;
            }
            bind-interface st0.110;
            establish-tunnels immediately;
        }
        vpn IPSEC-VPN-410 {
            ike {
                ipsec-policy IPSEC-POL;
                gateway IKE-GW-410;
            }
            bind-interface st0.410;
            establish-tunnels immediately;
        }
    }
    flow {
        nh-resolve-timeout 150;
        multicast-nh-resolve-retry 4;
        strict-packet-order;
        mcast-buffer-enhance;
        aging {
            early-ageout 30; high-watermark 90; low-watermark 70;
        }
        tcp-session {
            no-syn-check;
            no-sequence-check;
        }
        tcp-mss {
            all-tcp {
                mss 536;
            }
        }
    }
    zones {
        security-zone ZONE-1 {
            host-inbound-traffic {
                system-services {
                    ike;
                    ping;
                    snmp;
                    ssh;
                    dhcp;
                }
                protocols {
                    bfd;
                    ospf;
                    pim;
                    igmp;
                    vrrp;
                }
            }
            interfaces {
                ge-0/0/5.30;
                st0.110;
                st0.410;
                lo0.0;
                irb.12;
            }
            enable-reverse-reroute;
        }
    }
}

services {
    rpm {
        twamp {
            client {
                control-connection "TWAMP_HUB010R01"  {
                    persistent-results;
                    target-address 172.19.0.237;
                    test-count 1;
                    test-session "probe" {
                        target-address 172.19.0.237;
                        dscp-code-points cs7;
                        data-size 60;
                        probe-count 201;
                        probe-interval 1;
                        thresholds {
                            rtt  40000;
                            jitter-rtt 20000;
                            total-loss 2;
                        }
                        traps {
                            max-rtt-exceeded;
                            jitter-exceeded;
                            test-failure;
                        }
                    }
                }
            }
            client {
                control-connection "TWAMP_HUB010R02"  {
                    persistent-results;
                    target-address 172.18.0.237;
                    test-count 1;
                    test-session "probe" {
                        target-address 172.18.0.237;
                        dscp-code-points cs7;
                        data-size 60;
                        probe-count 201;
                        probe-interval 1;
                        thresholds {
                            rtt  40000;
                            jitter-rtt 20000;
                            total-loss 2;
                        }
                        traps {
                            max-rtt-exceeded;
                            jitter-exceeded;
                            test-failure;
                        }
                    }
                }
            }
        }
    }
}

policy-options {
	prefix-list INT      {
		apply-path "interfaces <*> unit <*> family inet address <*>"                   ;
	}
	prefix-list LOOPBACK {
		10.214.74.252/32;
	}
	prefix-list OTHERLOOPBACK {
		10.214.74.212/32;
    }
	prefix-list TUNNELS  {
		apply-path "interfaces st0 unit <*> family inet address <*>" ;
	}
	prefix-list MANAGER {
		10.0.0.0/24 ;
		10.0.1.0/24 ;
		10.1.233.0/24 ;
		10.1.237.0/24 ;
		10.2.233.0/24 ;
		10.2.237.0/24 ;
		10.3.233.0/24 ;
		10.3.237.0/24 ;
		10.4.233.0/24 ;
		10.4.237.0/24 ;
		10.5.233.0/24 ;
		10.5.237.0/24 ;
		10.6.233.0/24 ;
		10.6.237.0/24 ;
		10.7.233.0/24 ;
		10.7.237.0/24 ;
		145.1.17.0/24 ;
		10.214.1.236 ;
		10.214.1.237 ;
		10.214.1.238 ;
		10.214.1.239 ;
		10.214.2.236 ;
		10.214.2.237 ;
		10.214.2.238 ;
		10.214.2.239 ;
		10.214.2.86 ;
		10.214.10.236 ;
		10.214.10.237 ;
		10.214.10.238 ;
		10.214.10.239 ;
	}
	prefix-list SNMP-MANAGER {
		10.0.0.2 ;
		10.0.1.2 ;
		10.4.233.250;
		10.4.233.251;
		10.4.233.246;
		10.4.237.250;
		10.4.237.251;
		10.4.237.246;
		10.4.233.20 ;
		10.4.237.20  ;
		10.1.237.20 ;
		10.1.233.20    ;
		10.4.233.158 ;
		10.4.233.159 ;
		10.1.233.158 ;
		10.1.233.159 ;
		10.0.0.15 ;
		10.0.1.15 ;
		145.1.17.0/24 ;
	}
	prefix-list OTHERLAN  {
		10.214.0.0/16 ;
	}
	prefix-list NTP           {
		apply-path "system ntp server <*>"                                                        ;
	}
	prefix-list NTP-Lo        {
		apply-path "system ntp source-address <*>"                                                ;
	}
	prefix-list TWAMP-CLIENTS {
		apply-path "services rpm twamp server client-list <*> address <*>"                        ;
	}
	prefix-list TWAMP-SERVER  {
		apply-path "services rpm twamp client control-connection <*> target-address <*>"          ;
	}
	prefix-list BGP           {
		apply-path "protocols bgp group <*> neighbor <*>"                                         ;
	}
	prefix-list BGP-SRC       {
		apply-path "protocols bgp group <*> neighbor <*> local-address <*>"                       ;
	}
	prefix-list IKE-REMOTE    {
		apply-path "security ike gateway <*> address <*>"                                         ;
	}
	prefix-list IKE-LOCAL     {
		apply-path "security ike gateway <*> local-address <*>"                                   ;
	}
	prefix-list IPSEC-REMOTE {
		apply-path "security ike gateway <*> address <*>"       ;
	}
	prefix-list IPSEC-LOCAL  {
		apply-path "security ike gateway <*> local-address <*>" ;
	}
	prefix-list LAN {
		apply-path "interfaces irb unit <12> family inet address <*>" ;
	}
	policy-statement LAN-TO-OSPF {
		term 10 {
			from {
				protocol direct ;
				prefix-list LAN ;
			}
			then {
				accept          ;
			}
		}
	}
	policy-statement load-balancing-policy {
		then {
			load-balance per-packet ;
		}
	}
    policy-statement SPT_INFINITY_POLICY {
        term 10 {
            from {
                route-filter 228.0.0.0/8 orlonger;
            }
            then accept;
        }
        term 20 {
            then reject;
        }
    }
	policy-statement TARGETED-BROADCAST {
		from {
			protocol static                     ;
			route-filter 10.214.74.255/32 exact ;
		}
		then {
			external {
				type 1                   ;
			}
			accept                              ;
		}
	}
}
routing-options {
    interface-routes {
        rib-group inet RG-10;
    }
    static {
        route 192.168.115.50/32 {
            next-hop 192.168.115.61;
        }
        route 192.168.115.51/32 {
            next-hop 192.168.115.61;
        }
        route 0.1.2.3/32 {
            no-install;
            no-readvertise;
            preference 250;
            qualified-next-hop 172.19.0.237 {
                bfd-liveness-detection {
                    minimum-interval 300;
                    multiplier 3;
                    no-adaptation;
                    local-address 172.19.0.238;
                }
            }
            qualified-next-hop 172.18.0.237 {
                bfd-liveness-detection {
                    minimum-interval 300;
                    multiplier 3;
                    no-adaptation;
                    local-address 172.18.0.238;
                }
            }
        }
        route 10.214.74.255/32 {
            next-hop 10.214.74.5;
            no-install;
        }
    }
    rib-groups {
        RG-MCAST-RPF    {
            import-rib inet.2;
            export-rib inet.2;
        }
        RG-10           {
            import-rib inet.0;
            import-rib inet.2;
        }
    }
    router-id 10.214.74.252;
    forwarding-table {
        export load-balancing-policy;
    }
    multicast {
        resolve-request-holdtime 100;
        forwarding-cache {
                timeout 2;
            }
        route-update-priority-high;
        interface st0.110 {
            maximum-bandwidth 1000000;
        }
        interface st0.410 {
            maximum-bandwidth 1000000;
        }
    }
}
protocols {
    igmp {
        non-rfc-other-querier-present-timeout;
        query-interval 60;
        query-response-interval 1;
        query-last-member-interval 0.2;
        interface all {
            disable;
        }
        interface irb.12;
    }



    ospf {
        backup-spf-options {
            per-prefix-calculation {
                externals;
                summary;
            }
        }
        rib-group RG-10;
        external-preference 180;
        export LAN-TO-OSPF;
        export TARGETED-BROADCAST;
        area 10.214.74.0 {
            interface st0.110 {
                metric 300;
                apply-groups [ OSPF-INTERFACE OSPF-BFD OSPF-LFA ];
            }
        }
        area 10.214.74.0 {
            interface st0.410 {
                metric 300;
                apply-groups [ OSPF-INTERFACE OSPF-BFD OSPF-LFA ];
            }
        }
        area 10.214.74.0 {
            interface lo0.0 {
                passive;
            }
        }
    }

    pim {
        apply-groups PIM-RP-STATIC;
        rib-group inet RG-MCAST-RPF;
        synchronous-triggered-join-prune;
        spt-threshold {
            infinity SPT_INFINITY_POLICY;
        }

        interface st0.110 {
            apply-groups [ PIM-INTERFACE PIM-BFD ];
        }
        interface st0.410 {
            apply-groups [ PIM-INTERFACE PIM-BFD ];
        }
        interface irb.12 {
            apply-groups PIM-INTERFACE;
        }
        join-load-balance {
            automatic;
        }
    }

}

firewall {
    family inet {
        filter IGMP {
            term IGMP {
                from {
                    protocol igmp;
                }
                then {
                    count IGMP;
                    accept;
                }
            }
        }
        filter IKE {
            term IKE {
                from {
                    source-prefix-list      {
                        IKE-REMOTE;
                    }
                    destination-prefix-list {
                        IKE-LOCAL;
                    }
                    protocol udp;
                    destination-port 500;
                    source-port 500;
                }
                then {
                    count IKE;
                    accept;
                }
            }
        }
        filter OSPF {
            term OSPF {
                from {
                    source-prefix-list {
                        TUNNELS;
                    }
                    protocol ospf;
                }
                then {
                    count OSPF;
                    accept;
                }
            }
        }
        filter PIM  {
            term PIM            {
                from {
                    protocol pim;
                }
                then {
                    count PIM;
                    accept;
                }
            }
        }
        filter BGP  {
            term BGP            {
                from {
                    source-prefix-list      {
                        BGP;
                    }
                    destination-prefix-list {
                        BGP-SRC;
                    }
                    protocol tcp;
                    port bgp;
                }
                then {
                    count BGP;
                    accept;
                }
            }
        }
        filter ICMP {
            term ICMP-fragments {
                from {
                    is-fragment;
                    protocol icmp;
                }
                then {
                    discard;
                    log;
                }
            }
            term ICMP-allowed-1   {
                from {
                    protocol icmp;
                    icmp-type echo-reply;
                    icmp-type echo-request;
                    icmp-type time-exceeded;
                    icmp-type parameter-problem;
                }
                then {
                    policer 100K;
                    count ICMP;
                    accept;
                }
            }
            term ICMP-allowed-2   {
                from {
                    protocol icmp;
                    icmp-type unreachable;
                    icmp-code fragmentation-needed;
                }
                then {
                    policer 100K;
                    count ICMP;
                    accept;
                }
            }
        }
        filter SSH     {
            term SSH_Lo  {
                from {
                    source-prefix-list      {
                        MANAGER;
                    }
                    destination-prefix-list {
                        LOOPBACK;
                    }
                    protocol tcp;
                    port ssh;
                }
                then {
                    count SSH;
                    syslog;
                    accept;
                }
            }
            term SSH_Lan  {
                from {
                    source-prefix-list      {
                        LAN;
                        OTHERLAN;
                    }
                    destination-prefix-list {
                        LAN;
                        OTHERLOOPBACK;
                    }
                    protocol tcp;
                    port ssh;
                }
                then {
                    count SSH;
                    syslog;
                    accept;
                }
            }
        }
        filter SNMP    {
            term SNMP {
                from {
                    source-prefix-list      {
                        SNMP-MANAGER;
                    }
                    destination-prefix-list {
                        LOOPBACK;
                    }
                    protocol udp;
                    port snmp;
                }
                then {
                    policer 400K;
                    count SNMP;
                    accept;
                }
            }
        }
        filter NTP     {
            term NTP  {
                from {
                    source-prefix-list      {
                        NTP;
                        NTP-Lo;
                    }
                    destination-prefix-list {
                        INT;
                    }
                    protocol udp;
                    port ntp;
                }
                then {
                    policer 100K;
                    count NTP;
                    accept;
                }
            }
        }
        filter TWAMP {
            term TCP  {
                from {
                    prefix-list {
                        TWAMP-CLIENTS;
                        TWAMP-SERVER;
                    }
                    protocol tcp;
                    port 862;
                }
                then {
                    policer 400K;
                    count twamp-tcp;
                    accept;
                }
            }
            term UDP  {
                from {
                    prefix-list {
                        TWAMP-CLIENTS;
                        TWAMP-SERVER;
                    }
                    protocol udp;
                    port 10000-65535;
                }
                then {
                    policer 400K;
                    count twamp-udp;
                    accept;
                }
            }
        }
        filter BFD   {
            term BFD  {
                from {
                    prefix-list {
                        INT;
                    }
                    protocol udp;
                    source-port 49152-65535;
                    destination-port [ 3784-3785 4784 ];
                }
                then {
                    count bfd;
                    accept;
                }
            }
            term BFD2 {
                from {
                    prefix-list {
                        INT;
                    }
                    protocol udp;
                    destination-port 49152-65535;
                    source-port [ 3784-3785 4784 ];
                }
                then {
                    count bfd2;
                    accept;
                }
            }
        }
        filter DHCP  {
            term 10   {
                from {
                    protocol udp;
                    destination-port [ 67 68 ];
                }
                then {
                    policer 100K;
                    accept;
                }
            }
        }
        filter BAD-IP      {
            term OPTIONS {
                from {
                    ip-options [ loose-source-route strict-source-route ];
                }
                then {
                    discard;
                    log;
                }
            }
        }
        filter DISCARD-ALL {
            term DISCARD {
                then {
                    discard;
                    log;
                    syslog;
                    count discard;
                }
            }
        }
        filter VRRP {
            term VRRP {
                from {
                    protocol vrrp;
                }
                then {
                    accept;
                }
            }
        }
        filter RADIUS {
            term UDP {
                from {
                    protocol udp;
                    source-port [ 1812 1813 ];
                }
                then {
                    policer 100K;
                    accept;
                }
            }
        }
        filter RADIUS_OLD {
            term UDP {
                from {
                    protocol udp;
                    source-port [ 1645 1646 ];
                }
                then {
                    policer 100K;
                    accept;
                }
            }
        }
        filter IPSEC {
            term 1 {
                from {
                    source-prefix-list      {
                        IPSEC-REMOTE;
                    }
                    destination-prefix-list {
                        IPSEC-LOCAL;
                    }
                    protocol [ esp ah ];
                }
                then {
                    accept;
                }
            }
            term 2 {
                from {
                    source-prefix-list      {
                        IPSEC-LOCAL;
                    }
                    destination-prefix-list {
                        IPSEC-REMOTE;
                    }
                    protocol [ esp ah ];
                }
                then {
                    accept;
                }
            }
            term 3 {
                from {
                    source-prefix-list      {
                        IPSEC-REMOTE;
                    }
                    destination-prefix-list {
                        IPSEC-LOCAL;
                    }
                    protocol udp;
                    source-port 500;
                    destination-port 500;
                }
                then {
                    accept;
                }
            }
            term 4 {
                from {
                    source-prefix-list      {
                        IPSEC-LOCAL;
                    }
                    destination-prefix-list {
                        IPSEC-REMOTE;
                    }
                    protocol udp;
                    source-port 500;
                    destination-port 500;
                }
                then {
                    accept;
                }
            }
        }
        filter BH-INPUT {
            term IPSEC {
                filter IPSEC;
            }
            term DISCARD-ALL {
                filter DISCARD-ALL;
            }
        }
        filter DISCARD-TARGETED-BROADCAST {
            term 10 {
                from {
                    destination-address {
                        10.214.74.255/32;
                    }
                }
                then {
                    discard;
                }
            }
        }
        filter PASS-ALL {
            term 10 {
                then {
                    accept;
                }
            }
        }

        filter LAN-ONLY-SOURCE {
            term SRC {
                from {
                    source-address 10.214.74.0/24;
                }
                then {
                    accept;
                }
            }
        }
        filter DHCP-DISCOVER {
            term 10 {
                from {
                    source-address {
                        0.0.0.0/32;
                    }
                    protocol udp;
                    port dhcp;
                }
                then accept;
            }
        }
        filter LAN-INT-INPUT-FILTER {
            term DISCARD-TARGETED-BROADCAST {
                filter DISCARD-TARGETED-BROADCAST;
            }
            term DHCP-DISCOVER {
                filter DHCP-DISCOVER;
            }
            term LAN-ONLY-SOURCE      {
                filter LAN-ONLY-SOURCE;
            }
        }
        filter RE-INPUT {
            term VRRP         {
                filter VRRP;
            }
            term BAD-IP       {
                filter BAD-IP;
            }
            term IGMP         {
                filter IGMP;
            }
            term BFD          {
                filter BFD;
            }
            term IKE          {
                filter IKE;
            }
            term BGP          {
                filter BGP;
            }
            term OSPF         {
                filter OSPF;
            }
            term PIM          {
                filter PIM;
            }
            term ICMP         {
                filter ICMP;
            }
            term NTP          {
                filter NTP;
            }
            term SNMP         {
                filter SNMP;
            }
            term DHCP         {
                filter DHCP;
            }
            term SSH          {
                filter SSH;
            }
            term TWAMP        {
                filter TWAMP;
            }
            term RADIUS       {
                filter RADIUS;
            }
            term RADIUS_OLD   {
                filter RADIUS_OLD;
            }
            term DISCARD-ALL {
                filter DISCARD-ALL;
            }
        }
    }
    family inet6 {
        filter RE-INPUT-6 {
            term DISCARD {
                then discard;
            }
        }
    }
    policer 100K {
        if-exceeding {
            bandwidth-limit 100k;
            burst-size-limit 10k;
        }
        then discard;
    }
    policer 400K {
        if-exceeding {
            bandwidth-limit 400k;
            burst-size-limit 10k;
        }
        then discard;
    }
    policer 1M   {
        if-exceeding {
            bandwidth-limit 1m;
            burst-size-limit 15k;
        }
        then discard;
    }
}

event-options {
    generate-event {
        "Event_TWAMP" time-interval 900;
        "Event_TWAMP" no-drift;
    }
    policy rpd_bgp {
        events rpd_bgp_neighbor_state_changed;
        then {
            raise-trap;
        }
    }
    policy MinorAlarmSNMP_Trap {
        events SYSTEM;
        attributes-match {
            SYSTEM.message matches "Minor alarm set,.*";
        }
        then {
            raise-trap;
        }
    }
    policy "Policy_TWAMP" {
        events "Event_TWAMP";
        then {
            execute-commands {
                commands {
                    "request services rpm twamp start client TWAMP_HUB010R01";
                    "request services rpm twamp start client TWAMP_HUB010R02";
                }
            }
        }
    }
}


class-of-service {
    classifiers {
        inet-precedence CLASSIFIER-1 {
            forwarding-class FC0    {
                loss-priority high code-points 000;
                loss-priority low  code-points 001;
            }
            forwarding-class FC1    {
                loss-priority high code-points 010;
                loss-priority low  code-points 011;
            }
            forwarding-class FC2    {
                loss-priority high code-points 100;
                loss-priority low  code-points 110;
            }
            forwarding-class NETCOM {
                loss-priority high  code-points 101;
            }
            forwarding-class RTP    {
                loss-priority high  code-points 111;
            }
        }
    }

    forwarding-classes {
        queue 0 FC0;
        queue 1 FC1;
        queue 2 FC2;
        queue 4 NETCOM;
        queue 5 RTP;
        queue 3 NC;
    }

    interfaces {
        ge-0/0/0 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/1 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/2 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/5 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/6 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/7 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/8 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/9 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/10 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/11 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/12 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/13 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/14 {
            unit * {
                forwarding-class FC0;
            }
        }
        ge-0/0/15 {
            unit * {
                forwarding-class FC0;
            }
        }
        st0 {
            unit 110 {
                scheduler-map SCHEDULER-MAP-1;
                shaping-rate 1000000;
                classifiers {
                    inet-precedence CLASSIFIER-1;
                }
            }
        }
        st0 {
            unit 410 {
                scheduler-map SCHEDULER-MAP-1;
                shaping-rate 1000000;
                classifiers {
                    inet-precedence CLASSIFIER-1;
                }
            }
        }
        ge-0/0/5 {
            unit 30 {
                rewrite-rules {
                    inet-precedence REWRITE-RULE-IPPREC;
                }
            }
        }

        irb {
            unit * {
                forwarding-class FC0;
            }
            unit 12 {
                classifiers {
                    inet-precedence CLASSIFIER-1;
                }
            }
        }
    }

    rewrite-rules {
        inet-precedence REWRITE-RULE-IPPREC {
            forwarding-class FC0    {
                loss-priority high code-point 000;
                loss-priority  low code-point 001;
            }
            forwarding-class FC1    {
                loss-priority high code-point 001;
                loss-priority  low code-point 011;
            }
            forwarding-class FC2    {
                loss-priority high code-point 011;
                loss-priority  low code-point 101;
            }
            forwarding-class NETCOM {
                loss-priority  high code-point 101;
            }
            forwarding-class RTP    {
                loss-priority  high code-point 101;
            }
            forwarding-class NC {
                loss-priority low code-point 101;
                loss-priority high code-point 101;
            }
        }
    }

    scheduler-maps {
        SCHEDULER-MAP-1 {
            forwarding-class FC0 scheduler LOW;
            forwarding-class FC1 scheduler MEDIUM-LOW;
            forwarding-class FC2 scheduler MEDIUM-HIGH;
            forwarding-class NETCOM scheduler HIGH;
            forwarding-class RTP scheduler HIGH;
            forwarding-class NC scheduler STRICT-HIGH;
        }
    }

    schedulers {
        LOW         {
            priority low;
        }
        MEDIUM-LOW  {
            priority medium-low;
        }
        HIGH        {
            buffer-size percent 1;
            priority high;
        }
        MEDIUM-HIGH {
            priority medium-high;
        }
        STRICT-HIGH {
            priority strict-high;
        }
    }
}


chassis {
    dedicated-ukern-cpu;
    icmp {
        per-iff-rate-limit 200;
    }
    usb {
        storage {
            disable;
        }
    }
}

access {
    address-assignment {
        pool P2 {
            family inet {
                network 10.214.74.254/24;
                range r1 {
                    low 10.214.74.236;
                    high 10.214.74.239;
                }
                dhcp-attributes {
                    maximum-lease-time 28800;
                    router {
                        10.214.74.254;
                    }
                    name-server {
                        10.4.233.163;
                        ;
                    }
                }
            }
        }
    }
}

vlans {
    DEFAULT_VLAN {
        vlan-id 1;
    }
    UNUSED {
        vlan-id 11;
    }
    USED {
        vlan-id 12;
        l3-interface irb.12;
    }
    Monitoring {
        vlan-id 20;
    }
}

```

The output will be a list of set commands you can paste into your router

```
$ $ python junos_converter.py
usage: junos_converter.py [-h] [--ignore-annotations] --input INPUT
junos_converter.py: error: the following arguments are required: --input

$ python junos_converter.py --input example.conf
set version 14.1R1.10
set system host-name myrouter
set system root-authentication encrypted-password "$11111$VrloaKaj0$OwnE4.pHqnEGigmuLZQkZ/"
set system login user ckishimo uid 2000
set system login user ckishimo class super-user
set system login user ckishimo authentication encrypted-password "$1$YJ7i717qVpo8$myuAjTW/tkWlm6EudqcL4/"
protect system services
set system services ftp
set system services ssh
set system services telnet
set system services netconf ssh
deactivate system syslog
set system syslog user * any emergency
set system syslog file messages any notice
set system syslog file messages authorization info
set system syslog file interactive-commands interactive-commands any
set interfaces ge-0/0/1 vlan-tagging
set interfaces ge-0/0/2 vlan-tagging
top
annotate version "my configuration"
```

Or you can upload the output file to the Juniper device and use the 'load merge' command 

```
$ python junos_converter.py --input example.conf > example.set
$ scp example.set ckishimo@10.1.1.1:

[edit]
ckishimo@juniper-mx# load merge example.set    
```

Or you better use [napalm](https://github.com/napalm-automation/napalm)
```
$ cl_napalm_configure --strategy merge --user ckishimo --vendor junos 10.1.1.1 example.set
```

Notes
-----
- Annotations are supported. They will be listed at the end
   - Note "annotations" are not supported by Junos (ie: they will be lost when `show | display set`)
- Inactive blocks are supported (like "system syslog" in the example)
- Protect blocks are supported as well (like "system services" in the example)

Limitations
-----------
As we cannot distinguish a JUNOS keyword from a configuration value we cannot convert the other way around

