# Block adverts in Android mobile games that the more popular adlists don't catch

1. Log into the Pi-hole web interface
2. Click on 'Domains' on the left hand side menu:
   
  ![image](https://github.com/Dafterfly/Pi-hole-info/assets/17124333/fca45546-fe90-434e-82bc-13f76c8fb988)

3. Click on 'ReGex filter' and add `iads.unity3d.com` and a comment of your choice, then click 'Add to Blacklist'
   
![image](https://github.com/Dafterfly/Pi-hole-info/assets/17124333/2765233b-1647-472d-843c-1470374afbc1)

4. Repeat the above step but also add `mediation.unity3d.com` and any other requests that you notice

## Summary

To summarize, add the following domains as Regex filters as Blacklist entries:

```
iads.unity3d.com
mediation.unity3d.com
```

![image](https://github.com/Dafterfly/Pi-hole-info/assets/17124333/993e235a-a48c-401f-86bf-76427d5d4311)

