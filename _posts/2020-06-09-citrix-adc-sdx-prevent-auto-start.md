---
layout: blogcontent
title:  "Prevent auto-start of VPX VMs"
author: Jacob Wilson
comments: true
code: true
categories: ADC
permalink: /blog/:categories/:year/:month/:day/:title/
---

### History

During a SDX migration project it was useful to prevent VPX instances from auto-starting in the event that the SDX platform rebooted.  The primary reason for this was because I used the same IP addresses on the new instances that the old instances had and did not want to cause an IP conflict by ARPing over the new instance if the SDX platform rebooted.

### Process

SSH to the underlying XenServer host on your SDX appliance

Discover the VM UUIDs by executing the following command

~~~ bash
xe vm-list
~~~

Copy the uuid string from the VM you want to prevent from auto-starting

Execute the following command to set auto_poweron to false for that VM

~~~ bash
xe vm-param-set uuid=UUID other-config:auto_poweron=false
~~~

Verify the parameter was modified by executing

~~~ bash
xe vm-list uuid=UUID params=other-config
~~~

### End result

The selected VPX instance defined by UUID will no longer auto-start if the SDX platform is rebooted.
