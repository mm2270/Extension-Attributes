#!/bin/sh

if [[ "$( lsof -i :3283 | tail -1 | awk '{print $1}' )" == "ARDAgent" ]]; then
     echo "<result>On</result>"
else
     echo "<result>Off</result>"
fi
