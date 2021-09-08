pull request 09.aug.2021 see https://github.com/openwrt/openwrt/pull/4433

Note: only pure Ap mode or pure sta mode work good. both together as a repeater have errors and less strength.
update: 20.02.0RC4 https feed install is broken in my builds, only manually download and scp to the box & opkg install will work from the feeds. missing ssl.

# openwrt 21.02 build TRUNK 06. Aug 2021
---------------
ssh over wireless broken, use lan. for use with proprietary driver brcm-wl (the only working wifi-n driver for this device) you have to aditional edit some files

1. edit + add /etc/rc.local    , bring up wifi, during boot failed

        wifi up
   
2. edit + add one disabled wifi-interface to the end /etc/config/wireless , otherwhise buggy 2nd ap will be created. not necessary in sta mode

        config wifi-iface 'wifinet1'
            option device 'wl0'
            option mode 'ap'
            option ssid 'TrickToFixNasParams'
            option encryption 'none'
            option disabled '1'     
        
        
 3. edit + add to wifi-device section in /etc/config/wireless    , otherwhise the used mac makes the wifi instable.
 
        option macaddr '00:A2:....:38'    
 ---> use the wlan_mac one from the sticker -1 in the last number 
 of your w303v B in device section.       
 sticker('00:A2:...:39' --> use '00:A2:...:38')
        
 (maybe disable - option wmm 0 - will improve stability + also try  - option htmode 'HT40'  + select a fixed - option channel [1-11] + probably better antenna   - option txantenna '1' option rxantenna '2' + also - option noscan '1'  + and - option hwmode '11n') you can "wifi down" -> change and "wifi up" again to test
 
 4. optional - edit + add /lib/wifi/broadcom.sh try some settings e.g. wmm, htmode, and hwmode manually because of lack in the driver reading the config file settings. (makes the device more stable)

        #       config_get hwmode "$device" hwmode
        #       config_get htmode "$device" htmode
        local doth=0
        local wmm=0
        local hwmode=11n
        local htmode=HT40
        

# openwrt 21.02-0 RC4
------------------

same/ see 21.02 trunk, but you can install additional packages from the feed.

# openwrt 21.02-0 RC4 incl. LUCI
------------------

same/ see 21.02 trunk, but you can install additional packages from the feed and incl. minimal luci.
luci also over wireless broken, only via lan. Luci makes some performance loss in wireless too. maybe my build config were bad.

# openwrt 19.08
------------------

works out of the box, but has older brcm-wl driver, i think/realized 21.02 has more rangewide/coverage/stability because of mimo support.
