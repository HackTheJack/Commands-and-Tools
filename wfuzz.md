# USE GUIDE

*WFUZZ* can be used to look for hidden content, such as files and directories, within a web server, allowing to find further attack vectors.
This tool is included in Kali Linux.

---
Wfuzz contains some dictionaries, other larger and up to date open source word lists are:

* [fuzzdb](https://github.com/fuzzdb-project/fuzzdb)

* [seclists](https://github.com/danielmiessler/SecLists)

---

## Example usage to live out result 404

`wfuzz -u http://<IPTARGET>/FUZZ/ -w <YOURPATH>/raft-large-directories.txt --hc 404`

In this example we have used the SecLists file (Raft-large-direcotires.txt) contains directories' name.

-u URL and then we add FUZZ/ name to say wfuzz to change this name with the name present in the raft-largel-directories.txt file.

-w select our file.

--hc hide the result when we get page 404 as result.

```bash
wfuzz -u http://<IPTARGET>/FUZZ/ -w <YOURPATH>/raft-large-directories.txt --hc 404

********************************************************
* Wfuzz 2.4.5 - The Web Fuzzer                        *
********************************************************

Target: http://<IPTARGET>/FUZZ

Total requests: 62275
===================================================================
ID           Response   Lines    Word     Chars       Payload
===================================================================

000000002:   301        9 L      28 W     311 Ch      "images"
000000009:   301        9 L      28 W     307 Ch      "js"
000000015:   301        9 L      28 W     308 Ch      "css"
000000024:   301        9 L      28 W     311 Ch      "themes"
000000070:   200        9 L      28 W     312 Ch      "uploads"
000000276:   301        9 L      28 W     310 Ch      "fonts"
000004255:   200        478 L    1222 W   10932 Ch    ""
000022982:   301        9 L      28 W     312 Ch      "cdn-cgi"

-----------------------------------------------------------------------
```

## usage to live out result 403 and 404

`wfuzz -u http://<IPTARGET>/uploads/FUZZ -w <YOURPATH>/raft-large-files.txt --hc 404, 403`

```bash
wfuzz -u http://<IPTARGET>/uploads/FUZZ -w <YOURPATH>/raft-large-files.txt --hc 404, 403

********************************************************
* Wfuzz 2.4.5 - The Web Fuzzer                        *
********************************************************

Target: http://<IPTARGET>/uploads/FUZZ

Total requests: 62275
==================================================================
ID  Response   Lines      Word         Chars          Request
==================================================================

00429:  C=200      4 L        25 W      177 Ch    " - index.html"
00466:  C=301      9 L        28 W      319 Ch    " - db.php"
-----------------------------------------------------------------------
```

Another example how to find common files with wfuzz is:

`root@kali:~# wfuzz -w <YOURPATH>/common.txt http://<IPTARGET>/FUZZ.php`

### Sql injection

`wfuzz -c -z file,<YOURPATH>/SQL.txt --hs -d “username=admin&password=FUZZ” -u http://<IPTARGET>`

password

 -c : makes the output colourful, this is a personal choice.

 -z : payload/wordlist — the list you want it to use.

 --hs : ignore response containing Invalid, h in this instance being hide and s is actually the regex switch in this instance.

  -d : the post request.

  FUZZ : the section of the post I want to fuzz.

---

### Brute forcing:

`root@kali:~# -c -z file,<YOURPATH>/users.txt -z file,<YOURPATH>/password.txt --hs -d “username=FUZZ&password=FUZ2Z” -u http://<IPTARGET>`

We define two files (-z file,). The order of the files specified is important at this step. 
FUZZ takes the value present in the users.txt file. 
While, FUZ2Z takes the value present in the password.txt file.
user and password (we have to use two FUZZ values `FUZZ` and `FUZ2Z`)

---

### Tutti i comandi

To see the help:

```bash

wfuzz --help

********************************************************
* Wfuzz 2.4.5 - The Web Fuzzer                        *
*                                                      *
* Version up to 1.4c coded by:                         *
* Christian Martorella (cmartorella@edge-security.com) *
* Carlos del ojo (deepbit@gmail.com)                   *
*                                                      *
* Version 1.4d to 2.4.5 coded by:                     *
* Xavier Mendez (xmendez@edge-security.com)            *
********************************************************

Usage:  wfuzz [options] -z payload,params <url>

    FUZZ, ..., FUZnZ  wherever you put these keywords wfuzz will replace them with the values of the specified payload.
    FUZZ{baseline_value} FUZZ will be replaced by baseline_value. It will be the first request performed and could be used as a base for filtering.


Options:
    -h/--help           : This help
    --help              : Advanced help
    --version           : Wfuzz version details
    -e <type>           : List of available encoders/payloads/iterators/printers/scripts
   
    --recipe <filename>     : Reads options from a recipe
    --dump-recipe <filename>    : Prints current options as a recipe
    --oF <filename>         : Saves fuzz results to a file. These can be consumed later using the wfuzz payload.
   
    -c              : Output with colors
    -v              : Verbose information.
    -f filename,printer         : Store results in the output file using the specified printer (raw printer if omitted).
    -o printer                  : Show results using the specified printer.
    --interact          : (beta) If selected,all key presses are captured. This allows you to interact with the program.
    --dry-run           : Print the results of applying the requests without actually making any HTTP request.
    --prev              : Print the previous HTTP requests (only when using payloads generating fuzzresults)
   
    -p addr             : Use Proxy in format ip:port:type. Repeat option for using various proxies.
                      Where type could be SOCKS4,SOCKS5 or HTTP if omitted.
   
    -t N                : Specify the number of concurrent connections (10 default)
    -s N                : Specify time delay between requests (0 default)
    -R depth            : Recursive path discovery being depth the maximum recursion level.
    -L,--follow         : Follow HTTP redirections
    -Z              : Scan mode (Connection errors will be ignored).
    --req-delay N           : Sets the maximum time in seconds the request is allowed to take (CURLOPT_TIMEOUT). Default 90.
    --conn-delay N              : Sets the maximum time in seconds the connection phase to the server to take (CURLOPT_CONNECTTIMEOUT). Default 90.
   
    -A              : Alias for --script=default -v -c
    --script=           : Equivalent to --script=default
    --script=<plugins>      : Runs script's scan. <plugins> is a comma separated list of plugin-files or plugin-categories
    --script-help=<plugins>     : Show help about scripts.
    --script-args n1=v1,...     : Provide arguments to scripts. ie. --script-args grep.regex="<A href="(.*?)">"
   
    -u url                      : Specify a URL for the request.
    -m iterator         : Specify an iterator for combining payloads (product by default)
    -z payload          : Specify a payload for each FUZZ keyword used in the form of name[,parameter][,encoder].
                      A list of encoders can be used, ie. md5-sha1. Encoders can be chained, ie. md5@sha1.
                      Encoders category can be used. ie. url
                                  Use help as a payload to show payload plugin's details (you can filter using --slice)
    --zP <params>           : Arguments for the specified payload (it must be preceded by -z or -w).
    --slice <filter>        : Filter payload's elements using the specified expression. It must be preceded by -z.
    -w wordlist         : Specify a wordlist file (alias for -z file,wordlist).
    -V alltype          : All parameters bruteforcing (allvars and allpost). No need for FUZZ keyword.
    -X method           : Specify an HTTP method for the request, ie. HEAD or FUZZ
   
    -b cookie           : Specify a cookie for the requests. Repeat option for various cookies.
    -d postdata             : Use post data (ex: "id=FUZZ&catalogue=1")
    -H header           : Use header (ex:"Cookie:id=1312321&user=FUZZ"). Repeat option for various headers.
    --basic/ntlm/digest auth    : in format "user:pass" or "FUZZ:FUZZ" or "domain\FUZ2Z:FUZZ"
   
    --hc/hl/hw/hh N[,N]+        : Hide responses with the specified code/lines/words/chars (Use BBB for taking values from baseline)
    --sc/sl/sw/sh N[,N]+        : Show responses with the specified code/lines/words/chars (Use BBB for taking values from baseline)
    --ss/hs regex           : Show/hide responses with the specified regex within the content
    --filter <filter>       : Show/hide responses using the specified filter expression (Use BBB for taking values from baseline)
    --prefilter <filter>        : Filter items before fuzzing using the specified expression.
```

### Resource:

* [basic-usage](https://wfuzz.readthedocs.io/en/latest/user/basicusage.html)
* [user-guide](https://wfuzz.readthedocs.io/en/latest/)
* [advanced-usage](https://wfuzz.readthedocs.io/en/latest/user/advanced.html)
* [brute-force](https://securitybytes.io/wfuzz-using-the-web-brute-forcer-1bf8890db2f)
* [SQL-injection](https://medium.com/@scottc130/how-to-use-wfuzz-to-fuzz-web-applications-8594c11d59d1)
