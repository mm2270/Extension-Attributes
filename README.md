# Extension-Attributes
A collection of some Extension Attribute bash scripts for use with Casper Suite

####ARD Status  
This Extension Attributes reports on the status of Apple Remote Management (ARD) It will report either **On** or **Off** as a result. It will not report on any settings within the Remote Management framework, only if its currently enabled and listening for incoming connections.

####Current Wi-Fi Network  
This Extension Attribute reports on the current Wi-Fi network name, if available. If no Wi-Fi network is connected to, it will report **No current wireless network**  

####Free Disk Space (GBs)  
This Extension Attribute gathers the free disk space from the boot volume as reported by `df -H` (uses human readable notation)  
Although there are ways of gathering this information in bytes, kb or other increments and performing math calculations, I found these were not providing reliable results. The `df -H` command output seems to most closely match the free disk space as reported by Finder, so that is what this EA uses.

####Imaging Date (DeployStudio)
This Extension Attribute is designed primarily to work when Macs are imaged with DeployStudio, not with Casper Imaging. However, it can also be used with Casper Imaging, but may not provide the most accurate results.  
It is suggested that this EA be created and saved in Date format in your JSS.  
DeployStudio places a **ds_finalize.log** file on machines imaged that can provide an approximate date and time of imaging. This Extension Attribute uses `mdls` and the `kMDItemCreationDate` key from the log file to determine image date. If the log file is not present, it attempts to get the creation date from the `/Library/Application Support/JAMF/Receipts/` directory. A newly imaged Mac enrolled in Casper will not have the Receipts directory until the first policy applies to it.

####JAMF Waiting Room Contents  
This Extension Attribute reports on any .pkg, .mpkg or .dmg files in the `/Library/Application Support/JAMF/Waiting Room` directory. It will provide a list of any of these items in that directory, or report **Empty** if none are present. This can be useful as a way of seeing a birds eye view of cached packages in your environment.

####Java JRE Version
Reports back the full Java JRE version information. An example version string reported as of this writing could be:
`1.8.45.14`  
It will report `Not Installed` if the Java plug-in is not present.

####Last Boot Time (date formatted)
This Extension Attribute will report the last boot time of the Mac in proper date format for the Casper Suite. An example of output from this EA might be like:  
`2015-06-11 16:59:36`  
It is suggested that this EA be created and saved in Date format in your JSS. This will allow building Smart Groups that use criteria such as:  
`Last Boot Time | more than x days ago | 7`  
To capture all Macs with an uptime of greater than 7 days, as an example.

####Uptime (Hours)  
This Extension Attribute is similar to the above Last Boot Time one, except that it reports the total uptime calculated in hours, with a 2 number decimal. For example, a sample output from this EA may show:  
`12.25`  
This would indicate 12 hours and 15 minutes.

####Self Service Launch Count (X Days)
This Extension Attribute can roughly report on how many times the Self Service application (or any other application) was launched on a day basis, within a specified number of days. Note that because this uses `mdls` it is not possible to know how many times Self Service, or any other application, was launched within the same 24 hour period. Once 24 hours elapses, Spotlight condenses all previous uses into a single day entry.  
However, this EA can at least give you a generalized overview of how often within a week or month the application is used.  
Note that you can swap in a different application path within the EA to report on any other installed application on your client systems.
