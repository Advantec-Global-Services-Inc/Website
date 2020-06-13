---
layout: blogcontent
title:  "Prevent auto-start of VPX VMs"
comments: true
code: true
categories: ADC
permalink: /blog/:categories/:year/:month/:day/:title/
---

By default all VPX instances hosted on the SDX platform are configured to auto start. During a SDX migration project it was useful to prevent this behavior in the event that the SDX platform rebooted. The primary reason for this was because I used the same IP addresses on the new instances that the old instances had and did not want to cause an IP conflict by ARPing over the new instance if the SDX platform rebooted.

### Process

1. SSH to the underlying XenServer host on your SDX appliance

2. Discover the VM UUIDs by executing the following command

    ~~~ bash
    xe vm-list
    ~~~

    *Note: this command will list all of the VMs on the appliance*

3. Copy the UUID string from the VM you want to prevent from auto-starting

4. Execute the following command to set auto_poweron to false for that VM

    ~~~ bash
    xe vm-param-set uuid=yourUUID other-config:auto_poweron=false
    ~~~

    *Note: yourUUID will be populated with the UUID you copied in step 3*

5. Verify the parameter was modified by executing

    ~~~ bash
    xe vm-list uuid=yourUUID params=other-config
    ~~~

### End result

The selected VPX instance defined by UUID will no longer auto-start if the SDX platform is rebooted.
