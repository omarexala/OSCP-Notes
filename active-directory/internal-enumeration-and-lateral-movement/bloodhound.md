# BloodHound

### Linux

**Running bloodhound from Linux host**

```
bloodhound-python -h
```

**Running bloodhound**

{% code overflow="wrap" %}
```
sudo bloodhound-python -u 'forend' -p 'Klmcargo2' -ns 172.16.5.5 -d inlanefreight.local -c all 
```
{% endcode %}

**Turn on neo4j**

```
sudo neo4j start
```

**File Transfer:**

{% code overflow="wrap" %}
```
xfreerdp /u:stephanie /p:'LegmanTeamBenzoin!!' /v:192.168.193.75 /drive:test,/home/kali/Documents/Tools
```
{% endcode %}

**Zipping .json created from SharpHound**

```
zip -r ilfreight_bh.zip *.json
```

***

### Windows

**Running SharpHound**

```
.\SharpHound.exe --help
```

**Creating zip file**&#x20;

```
.\SharpHound.exe -c All --zipfilename ILFREIGHT
```



