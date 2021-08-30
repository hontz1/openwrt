pull request 09.aug.2021 see https://github.com/openwrt/openwrt/pull/4433

# openwrt 21.02 build TRUNK 06. Aug 2021
---------------
for use with proprietary driver brcm-wl (the only working wifi-n driver for this device) you have to aditional edit some files

1. edit + add /etc/rc.local    , bring up wifi, during boot failed

        sleep 10
        wifi down
        sleep 10
        wifi up
   
2. edit + add one disabled wifi-interface to the end /etc/config/wireless , otherwhise buggy 2nd ap will be created.

        config wifi-iface 'wifinet1'
            option device 'wl0'
            option mode 'ap'
            option ssid 'TrickToFixNasParams'
            option encryption 'none'
            option disabled '1'     
        
        
 2. edit + add to wifi-device section in /etc/config/wireless    , otherwhise the used mac makes the wifi instable.
 
        option macaddr '00:A2:....:38'    ---> use the wlan_mac one from the sticker of your w303v B
        
        (maybe disable - option wmm 0 - will improve stability -  + also try  - option htmode 'ht40' -  + select a fixed - option channel [1-11] -  )
        

# openwrt 21.02-0 RC4
------------------

same/ see 21.02 trunk, but you can install additional packages from the feed.

# openwrt 21.02-0 RC4 incl. LUCI
------------------

same/ see 21.02 trunk, but you can install additional packages from the feed and incl. minimal luci.

# openwrt 19.08
------------------

works out of the box, but has older brcm-wl driver, i think/realized 21.02 has more rangewide/coverage/stability because of mimo support.
