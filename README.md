# openwrt 21.02 build 06. Aug 2021
---------------

1. edit + add /etc/rc.local    , bring up wifi, during boot failed

        sleep 10
        wifi down
        sleep
        wifi up
   
2. edit + add disabled wif to the end /etc/config/wireless , otherwhise buggy 2nd ap will be created.

        config wifi-iface 'wifinet1'
            option device 'wl0'
            option mode 'ap'
            option ssid 'TrickToFixNasParams'
            option encryption 'none'
            option disabled '1'     
        
        
 2. edit + add to /etc/config/wireless    , otherwhise the used mac makes the wifi instable.
 
        option macaddr '00:....:38'    ---> use the wlan_mac one from the sticker of your w303v
        
        (maybe disable - option wmm 0 - will improve stability -  + also try  - option htmode 'ht40' -)
        


# openwrt 19.08
------------------

works out of the box, but has older brcm-wl driver, i think 21.02 has more rangewide.
