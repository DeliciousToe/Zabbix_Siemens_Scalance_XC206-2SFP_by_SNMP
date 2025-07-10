SCALANCE XC(206-2SFP) by SNMP - Zabbix Template

This repository provides a Zabbix template for monitoring Siemens SCALANCE XC(206-2SFP) devices via SNMP. It offers comprehensive insights into the device's system health, network interfaces, and various operational parameters.

Features:
System Information: Gathers basic system details like name, description, location, contact, uptime, and object ID.

  -CPU Load Monitoring: Tracks the CPU utilization of the device.
  
  -Memory Usage Monitoring: Monitors the total, used, and free memory, as well as buffer and cache memory.
  
  -Temperature Monitoring: Provides temperature readings for the device.
  
  -Power Supply Status: Checks the operational status of power supply units (PSUs).
  
  -Fan Status Monitoring: Monitors the operational status of fans (if present).
  
  -Network Interface Discovery: Automatically discovers network interfaces, including Ethernet, Fiber, and Management interfaces.
  
  -Detailed Interface Statistics: Collects inbound and outbound traffic, unicast, multicast, and broadcast packets, and error/discard counts for each discovered interface.
  
  -Interface Status Monitoring: Monitors the administrative and operational status of network interfaces.
  
  -Pre-processing: Utilizes Zabbix pre-processing for data transformation (e.g., converting centiseconds to uptime, calculating change per second for rates).
  
  -Configurable Triggers: Includes predefined triggers for critical conditions such as high CPU load, low memory, high temperature, power supply/fan failures, and interface issues.
  
  -Visualizations: Provides graph prototypes for various metrics like CPU utilization, memory usage, temperature, and network traffic.
  


Requirements

  - Zabbix Server (version 7.0 or higher recommended). 
  - Siemens SCALANCE XC(206-2SFP) device with SNMP agent enabled. 
  - SNMP community string configured on the SCALANCE device and accessible from the Zabbix server.

Installation:
Download the Template: Download the SCALANCE XC(206-2SFP) by SNMP.xml file from this repository.    
    Import into Zabbix: 
        - Navigate to Configuration -> Templates in your Zabbix frontend. 
        - Click Import in the top right corner.   
        - Click Browse and select the SCALANCE XC(206-2SFP) by SNMP.xml file. 
        - Click Import.   
    Link to Host:   
        - Go to Configuration -> Hosts.   
        - Select the SCALANCE XC(206-2SFP) host you wish to monitor, or create a new host.    
        - Go to the Templates tab.    
        - In the Link new templates section, search for SCALANCE XC(206-2SFP) by SNMP and select it.  
        - Click Add, then click Update on the host configuration page.    
    Configure SNMP on Host: 
        - Ensure the host's SNMP interface is correctly configured (IP address and SNMP community string).    
        - If using SNMPv3, configure the credentials accordingly on the host.

Monitored Items:
The template includes the following items for monitoring:

System Information

- System Name: snmp.get[sysName.0]
- System Description: snmp.get[sysDescr.0]
- System Location: snmp.get[sysLocation.0]
- System Contact: snmp.get[sysContact.0]
- System Uptime: snmp.get[sysUpTimeInstance] (converted to uptime)
- System Object ID: snmp.get[sysObjectID.0]

CPU

- CPU Utilization: snmp.get[cpu_utilization.0]

Memory

- Total Memory: snmp.get[total_memory.0]
- Used Memory: snmp.get[used_memory.0]
- Free Memory: snmp.get[free_memory.0]
- Buffer Memory: snmp.get[buffer_memory.0]
- Cache Memory: snmp.get[cache_memory.0]

Environment

- Temperature: snmp.get[temperature.0]

Power Supply

- Power Supply Operational Status PSU{ #SNMPINDEX }: snmp.get[power_supply_status.{#SNMPINDEX}]

Fans

- Fan Operational Status Fan{ #SNMPINDEX }: snmp.get[fan_status.{#SNMPINDEX}]

Network Interface Discovery (via Low-Level Discovery)
For each discovered network interface, the following items are created:

- Interface {#IFNAME}({#IFALIAS}): Admin status: net.if.admin.status[ifAdminStatus.{#SNMPINDEX}]
- Interface {#IFNAME}({#IFALIAS}): Inbound broadcast packets: net.if.in.bcast[ifHCInBroadcastPkts.{#SNMPINDEX}] (packets per second)
- Interface {#IFNAME}({#IFALIAS}): Inbound discards: net.if.in.discards[ifInDiscards.{#SNMPINDEX}] (discards per second)
- Interface {#IFNAME}({#IFALIAS}): Inbound errors: net.if.in.errors[ifInErrors.{#SNMPINDEX}] (errors per second)
- Interface {#IFNAME}({#IFALIAS}): Inbound multicast packets: net.if.in.mcast[ifHCInMulticastPkts.{#SNMPINDEX}] (packets per second)
- Interface {#IFNAME}({#IFALIAS}): Inbound unicast packets: net.if.in.ucast[ifHCInUcastPkts.{#SNMPINDEX}] (packets per second)
- Interface {#IFNAME}({#IFALIAS}): Inbound traffic: net.if.in[ifHCInOctets.{#SNMPINDEX}] (bytes per second)
- Interface {#IFNAME}({#IFALIAS}): Last change: net.if.lastchange[ifLastChange.{#SNMPINDEX}] (converted to uptime)
- Interface {#IFNAME}({#IFALIAS}): MTU: net.if.mtu[ifMtu.{#SNMPINDEX}] (bytes)
- Interface {#IFNAME}({#IFALIAS}): Outbound broadcast packets: net.if.out.bcast[ifHCOutBroadcastPkts.{#SNMPINDEX}] (packets per second)
- Interface {#IFNAME}({#IFALIAS}): Outbound discards: net.if.out.discards[ifOutDiscards.{#SNMPINDEX}] (discards per second)
- Interface {#IFNAME}({#IFALIAS}): Outbound errors: net.if.out.errors[ifOutErrors.{#SNMPINDEX}] (errors per second)
- Interface {#IFNAME}({#IFALIAS}): Outbound multicast packets: net.if.out.mcast[ifHCOutMulticastPkts.{#SNMPINDEX}] (packets per second)
- Interface {#IFNAME}({#IFALIAS}): Outbound unicast packets: net.if.out.ucast[ifHCOutUcastPkts.{#SNMPINDEX}] (packets per second)
- Interface {#IFNAME}({#IFALIAS}): Outbound traffic: net.if.out[ifHCOutOctets.{#SNMPINDEX}] (bytes per second)
- Interface {#IFNAME}({#IFALIAS}): Physical address: net.if.physaddr[ifPhysAddress.{#SNMPINDEX}]
- Interface {#IFNAME}({#IFALIAS}): Speed: net.if.speed[ifSpeed.{#SNMPINDEX}] (bits per second)
- Interface {#IFNAME}({#IFALIAS}): Operational status: net.if.status[ifOperStatus.{#SNMPINDEX}]
- Interface {#IFNAME}({#IFALIAS}): Type: net.if.type[ifType.{#SNMPINDEX}]

Triggers
The template includes the following triggers:

System Triggers

- System Contact is not set on {HOST.NAME}: Triggers if sysContact.0 is empty or not available for 1 hour (WARNING).
- System Location is not set on {HOST.NAME}: Triggers if sysLocation.0 is empty or not available for 1 hour (WARNING).
- System Object ID has changed on {HOST.NAME}: Triggers if sysObjectID.0 changes (INFO).
- System services have changed on {HOST.NAME}: Triggers if sysServices.0 changes (INFO).
- High CPU utilization on {HOST.NAME}: Triggers if CPU utilization exceeds 90% (HIGH).
- Insufficient free memory on {HOST.NAME}: Triggers if free memory is less than 10MB (HIGH).
- High temperature on {HOST.NAME}: Triggers if the device temperature exceeds 70°C (HIGH).
- Critical temperature on {HOST.NAME}: Triggers if the device temperature exceeds 80°C (DISASTER).

Power Supply Triggers (Prototypes)

- Power supply PSU{#SNMPINDEX} on {HOST.NAME} is down: Triggers if the power supply operational status is "powerOff" (HIGH).

Fan Triggers (Prototypes)

-  Fan Fan{#SNMPINDEX} on {HOST.NAME} is down: Triggers if the fan operational status is "powerOff" (HIGH).

Network Interface Triggers (Prototypes)

- High inbound broadcast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if inbound broadcast packets exceed 500 pps (WARNING).
- High inbound multicast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if inbound multicast packets exceed 1000 pps (WARNING).
- High inbound unicast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if inbound unicast packets exceed 10000 pps (WARNING).
- High outbound broadcast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if outbound broadcast packets exceed 500 pps (WARNING).
- High outbound multicast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if outbound multicast packets exceed 1000 pps (WARNING).
- High outbound unicast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if outbound unicast packets exceed 10000 pps (WARNING).
- Interface {#IFNAME}({#IFALIAS}) is down: Triggers if the operational status of the interface is "down" (HIGH).
- Interface {#IFNAME}({#IFALIAS}) has low speed (current: {ITEM.VALUE}): Triggers if the interface speed is less than 100 Mbps while operational (AVERAGE).

Discovery Rules:
Network interfaces discovery: This rule uses SNMP to discover network interfaces (Ethernet, Fiber, and Management) and create associated items, triggers, and graphs.
    SNMP OID: discovery[{#SNMP_OID},1.3.6.1.2.1.2.2.1.2,{#IFALIAS},1.3.6.1.2.1.31.1.1.1.18,{#IFNAME},1.3.6.1.2.1.31.1.1.1.1,{#IFDESCR},1.3.6.1.2.1.2.2.1.2,{#IFTYPE},1.3.6.1.2.1.2.2.1.3,{#IFSPEED},1.3.6.1.2.1.2.2.1.5,{#IFOPERSTATUS},1.3.6.1.2.1.2.2.1.8,{#IFADMINSTATUS},1.3.6.1.2.1.2.2.1.7]
    Key: net.if.discovery
    Delay: 1 hour
Power Supply discovery: Discovers power supply units on the device.
    SNMP OID: discovery[{#SNMP_OID},1.3.6.1.4.1.4116.1.1.1.3.1.1.1]
    Key: power.supply.discovery
    Delay: 1 hour
Fan discovery: Discovers fan units on the device.
    SNMP OID: discovery[{#SNMP_OID},1.3.6.1.4.1.4116.1.1.1.3.1.2.1]
    Key: fan.discovery
    Delay: 1 hour

Graphs
The template includes the following graphs:

System Graphs

- CPU Utilization: Visualizes the CPU utilization.
- Memory Usage: Visualizes total, used, free, buffer, and cache memory.
- Temperature: Visualizes the device's temperature.

Network Interface Graphs (Prototypes)

- Interface {#IFNAME}({#IFALIAS}): Broadcast packets: Visualizes inbound and outbound broadcast packets. 
- Interface {#IFNAME}({#IFALIAS}): Errors and discards: Visualizes inbound and outbound errors and discards.
- Interface {#IFNAME}({#IFALIAS}): Network traffic: Visualizes inbound and outbound network traffic in Bps.
- Interface {#IFNAME}({#IFALIAS}): Speed: Visualizes the interface speed in bps.- 
- Interface {#IFNAME}({#IFALIAS}): Unicast packets: Visualizes inbound and outbound unicast packets.

Value Maps:
The template utilizes the following value maps for better readability of SNMP integer values:

- SNMP interface status (ifAdminStatus): Maps numerical administrative status to "up", "down", "testing".
- SNMP interface status (ifOperStatus): Maps numerical operational status to "up", "down", "testing", "unknown", "dormant", "notPresent", "lowerLayerDown".
- SNMP interface type (ifType): Maps numerical interface types to "other", "ethernetCsmacd", "iso88025TokenRing", "loopback", "fddi", "basicISDN", "primaryISDN", "propPointToPointSerial", "ppp", "softwareLoopback", "eon", "ethernet3Mbit", "fastEther", "isdn", "sync", "isdnV110", "isdnV120", "rs232", "parallel", "arcnet", "arcnetPlus", "frameRelay", "atm", "hssi", "aal5", "sonet", "atmDxi", "atmFuni", "atmIli", "atmLec", "atmMar", "iso88024TokenBus", "iso88026Man", "digital", "hippi", "hdsl", "sdl", "fastEtherFX", "channel", "ieee80211", "tunnel", "longDistance", "mhp", "e1", "e3", "t1", "t3", "cctEmul", "fibreChannel", "h323Gatekeeper", "h323Proxy", "ibm370Parallel", "hipppiInterface", "hipppiLink", "ultra", "ds0", "ds1", "ds3", "e2", "e4", "g703at1544k", "g703at2048k", "g703at64k", "sdlc", "qllc", "apl", "smds", "v35", "x21", "isdnS", "isdnU", "lapb", "modem", "v24", "v50", "v51", "v52", "v53", "v54", "v55", "v56", "v57", "v58", "v59", "v60", "v61", "v62", "v63", "v64", "v65", "v66", "v67", "v68", "v69", "v70", "v71", "v72", "v73", "v74", "v75", "v76", "v77", "v78", "v79", "v80", "v81", "v82", "v83", "v84", "v85", "v86", "v87", "v88", "v89", "v90", "v91", "v92", "v93", "v94", "v95", "v96", "v97", "v98", "v99", "v100", "v101", "v102", "v103", "v104", "v105", "v106", "v107", "v108", "v109", "v110", "v111", "v112", "v113", "v114", "v115", "v116", "v117", "v118", "v119", "v120", "v121", "v122", "v123", "v124", "v125", "v126", "v127", "v128", "v129", "v130", "v131", "v132", "v133", "v134", "v135", "v136", "v137", "v138", "v139", "v140", "v141", "v142", "v143", "v144", "v145", "v146", "v147", "v148", "v149", "v150", "v151", "v152", "v153", "v154", "v155", "v156", "v157", "v158", "v159", "v160", "v161", "v162", "v163", "v164", "v165", "v166", "v167", "v168", "v169", "v170", "v171", "v172", "v173", "v174", "v175", "v176", "v177", "v178", "v179", "v180", "v181", "v182", "v183", "v184", "v185", "v186", "v187", "v188", "v189", "v190", "v191", "v192", "v193", "v194", "v195", "v196", "v197", "v198", "v199", "v200", "v201", "v202", "v203", "v204", "v205", "v206", "v207", "v208", "v209", "v210", "v211", "v212", "v213", "v214", "v215", "v216", "v217", "v218", "v219", "v220", "v221", "v222", "v223", "v224", "v225", "v226", "v227", "v228", "v229", "v230", "v231", "v232", "v233", "v234", "v235", "v236", "v237", "v238", "v239", "v240", "v241", "v242", "v243", "v244", "v245", "v246", "v247", "v248", "v249", "v250", "v251", "v252", "v253", "v254", "v255", "v256", "v257", "v258", "v259", "v260", "v261", "v262", "v263", "v264", "v265", "v266", "v267", "v268", "v269", "v270", "v271", "v272", "v273", "v274", "v275", "v276", "v277", "v278", "v279", "v280", "v281", "v282", "v283", "v284", "v285", "v286", "v287", "v288", "v289", "v290", "v291", "v292", "v293", "v294", "v295", "v296", "v297", "v298", "v299", "v300", "v301", "v302", "v303", "v304", "v305", "v306", "v307", "v308", "v309", "v310", "v311", "v312", "v313", "v314", "v315", "v316", "v317", "v318", "v319", "v320", "v321", "v322", "v323", "v324", "v325", "v326", "v327", "v328", "v329", "v330", "v331", "v332", "v333", "v334", "v335", "v336", "v337", "v338", "v339", "v340", "v341", "v342", "v343", "v344", "v345", "v346", "v347", "v348", "v349", "v350", "v351", "v352", "v353", "v354", "v355", "v356", "v357", "v358", "v359", "v360", "v361", "v362", "v363", "v364", "v365", "v366", "v367", "v368", "v369", "v370", "v371", "v372", "v373", "v374", "v375", "v376", "v377", "v378", "v379", "v380", "v381", "v382", "v383", "v384", "v385", "v386", "v387", "v388", "v389", "v390", "v391", "v392", "v393", "v394", "v395", "v396", "v397", "v398", "v399", "v400", "v401", "v402", "v403", "v404", "v405", "v406", "v407", "v408", "v409", "v410", "v411", "v412", "v413", "v414", "v415", "v416", "v417", "v418", "v419", "v420", "v421", "v422", "v423", "v424", "v425", "v426", "v427", "v428", "v429", "v430", "v431", "v432", "v433", "v434", "v435", "v436", "v437", "v438", "v439", "v440", "v441", "v442", "v443", "v444", "v445", "v446", "v447", "v448", "v449", "v450", "v451", "v452", "v453", "v454", "v455", "v456", "v457", "v458", "v459", "v460", "v461", "v462", "v463", "v464", "v465", "v466", "v467", "v468", "v469", "v470", "v471", "v472", "v473", "v474", "v475", "v476", "v477", "v478", "v479", "v480", "v481", "v482", "v483", "v484", "v485", "v486", "v487", "v488", "v489", "v490", "v491", "v492", "v493", "v494", "v495", "v496", "v497", "v498", "v499", "v500", "v501", "v502", "v503", "v504", "v505", "v506", "v507", "v508", "v509", "v510", "v511", "v512", "v513", "v514", "v515", "v516", "v517", "v518", "v519", "v520", "v521", "v522", "v523", "v524", "v525", "v526", "v527", "v528", "v529", "v530". 
- Siemens Power Supply Status: Maps numerical status to "unknown", "running", "powerOff".
- Siemens Fan Status: Maps numerical status to "unknown", "running", "powerOff".
