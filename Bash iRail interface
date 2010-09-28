#!/bin/bash
# by Pieter Colpaert & others
# http://project.irail.be
 
from=${1-Harelbeke}
[ $# -eq 0 ] && { echo "Usage: $0 from to" ; exit 1; }
to=${2-Gent Sint Pieters}
[ $# -eq 0 ] && { echo "Usage: $0 from to" ; exit 1; }
 
 
wget "http://api.irail.be/connections/?from=$from&to=$to&results=1&lang=EN" -O irail.xml --user-agent="iRail bash interface" 2>/dev/null
 
IFS=\>
i=0
while read -d \< element content ; do {
        if [[ $element == time* ]]
        then
            echo ${element:16:16}
        fi
        if [[ $element == platform* ]]
        then
            [[ $i -eq "0" ]] && { echo Departure ; } || { echo Arrival ; }
            echo "platform $content"
        fi
        #echo $element : $content
        i=$i+1
        [[ i -eq 2 ]] && i=0
} done < irail.xml