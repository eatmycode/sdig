`sdig` (aka. `SupaDig`)
---

Simply Put... The `dig` Utility On Steroids.

A wrapper for the dig command-line tool that Digs up full existing DNS details on any valid domain:

   + Checks if root domain and/or provides the root domain.
   + Provides as quick look at WHOIS: [Registrar, Nameservers + IPS, Expiration] (if available).
   + Digs for propagated and visible zone records.
   + Digs for propagated and cached entries in Level 3's & Google's public DNS
   + Digs for SOA serials for comparison.
   + Digs for the respective PTR's on associated IP's.
   + Explicitly displays where web traffic is directed.
   + Explicitly displays where mail traffic is directed.
   + Provides the owner of associated IP's.

## Requirements

Any Linux Based OS/Virtual Environment

`AND`

dnsutils package

`AND`

jwhois package

---

Why dnsutils?

The dnsutils package contains dig (domain information groper), which is a flexible tool for interrogating DNS name servers. It performs DNS lookups and displays the answers that are returned from the name server(s) that were queried. Most DNS administrators use dig to troubleshoot DNS problems because of its flexibility, ease of use and clarity of output. Other lookup tools tend to have less functionality than dig.


Why jwhois?

jwhois is an Internet Whois client that queries hosts for information about a domain according to RFC 954 - NICNAME/WHOIS. 

---

* On a production webserver, typically both would already be installed (see your host if you are unsure).

* If using on your local box and you dont have the dnsutils and/or jwhois package insatlled, then get it.

* A quick check:

		# Open up a linux terminal and type:

		~$ which dig whois

		# If you have it installed, you should see something similar to:

		~$ which dig whois
		/usr/bin/dig
		/usr/bin/whois

		# If you get nothing in return or see somthing like /usr/bin/which: no {SOFTWARE_NAME} in (/usr/local/bin:.....
		# for either one, then you dont have it (if not both) installed.

## Configuration

Just drop `sdig` in your scripts, bin, or executable dir:

    ~$ cd /place/to/where/you/downloaded/sdig
	~$ mv sdig /path/to/your/executable/scripts/

...or create a symlink to `sdig` in your scripts, bin, or executable dir:

    ~$ cd /path/to/your/executable/scripts/
	~$ ln -s /place/to/where/you/downloaded/sdig ./sdig

**Done!**

## How To `sdig`


	~$ sdig

                                      _ _       
                                     | |_|      
              ___ _  _ ____  ____  __| |_  ____ 
             / __| || |  _ \/ _  \/ _  | |/ _  \
             \__ \ || | |_| ||_| | |_| | | |_| |
             |___/___/| .__/\__/_|\____|_|\__  | 1.0 
                      | |                  __| | @eatmycode
                      |_|                 |____/


	   :usage:   sdig <domain.tld> [or]
	             sdig <email@domain.tld> [or]
	             sdig <http://hostname.tld/some/page.ext> [or]
	             sdig --about [or]
	             sdig --help
	             
	      
	      
	             
	~$ sdig eatmycode.pro


                                      _ _       
                                     | |_|      
              ___ _  _ ____  ____  __| |_  ____ 
             / __| || |  _ \/ _  \/ _  | |/ _  \
             \__ \ || | |_| ||_| | |_| | | |_| |
             |___/___/| .__/\__/_|\____|_|\__  | 1.0 
                      | |                  __| | @eatmycode
                      |_|                 |____/



	  EATMYCODE.PRO - 2nd-level! (has 1 dot)
	|----------------------------------------------------------------|
	  Root Domain: eatmycode.pro
	         Zone: eatmycode.pro
	
	
	
	  CURRENT WHOIS
	|----------------------------------------------------------------|
	  Registration & Nameservers Only:
	     Registrar:	RegistryPRO
	     Sponsor:	Name.com LLC (R2371-PRO)
	     Expires:	2015-04-10
	     Name server:	ns1.marquelmedia.net	192.34.62.120
	     Name server:	ns2.marquelmedia.net	198.199.103.108
	
	
	
	  ZONE RECORDS (has propagated)
	|----------------------------------------------------------------|
	  Currently Visible:
	     eatmycode.pro.		6520 IN	NS ns1.marquelmedia.net.
	     eatmycode.pro.		6520 IN	NS ns2.marquelmedia.net.
	
	
	
	  PUBLIC DNS (what presumably has propagated & been cached)
	|----------------------------------------------------------------|
	  Level3's Public DNS:
	     @a.resolvers: 198.199.102.252 [ PTR: lb2.marquelmedia.net ] 
     	     - Serial: 2013051802
	     
	     @a.resolvers: 198.199.82.212 [ PTR: lb1.marquelmedia.net ] 
     	     - Serial: 2013051802
	     
	     @b.resolvers: 198.199.82.212 [ PTR: lb1.marquelmedia.net ] 
     	     - Serial: 2013051802
	     
	     @b.resolvers: 198.199.102.252 [ PTR: lb2.marquelmedia.net ] 
     	     - Serial: 2013051802
	     
	     @c.resolvers: 198.199.102.252 [ PTR: lb2.marquelmedia.net ] 
     	     - Serial: 2013051802
	     
	     @c.resolvers: 198.199.82.212 [ PTR: lb1.marquelmedia.net ] 
     	     - Serial: 2013051802
	     

	  Google's Public DNS:
	     @google-public-dns-a: 198.199.82.212 [ PTR: lb1.marquelmedia.net ] 
     	     - Serial: 2013051802
	     
	     @google-public-dns-a: 198.199.102.252 [ PTR: lb2.marquelmedia.net ] 
     	     - Serial: 2013051802
	     
	     @google-public-dns-b: 198.199.82.212 [ PTR: lb1.marquelmedia.net ] 
     	     - Serial: 2013051802
	     
	     @google-public-dns-b: 198.199.102.252 [ PTR: lb2.marquelmedia.net ] 
     	     - Serial: 2013051802
     
	
	
	  WHERE WEB TRAFFIC GOES
	|----------------------------------------------------------------|
	  Active A Record(s):
	      A: 198.199.82.212 [ PTR: lb1.marquelmedia.net ]
		     - IP Owned by: Digital Ocean, Inc.
	
	      A: 198.199.102.252 [ PTR: lb2.marquelmedia.net ]
		     - IP Owned by: Digital Ocean, Inc.
	
	
	
	  WHERE MAIL TRAFFIC GOES
	|----------------------------------------------------------------|
	  Active MX Record(s):
	     MX: 0 mail.marquelmedia.net => 198.199.82.196 [ PTR: mail.marquelmedia.net ]
		     - IP Owned by: Digital Ocean, Inc.

## Limitations

   + Currently missing support for all of the `new vanity` TLD's recently released to the market.
   + Depending on the registrar, some WHOIS records cannot be parsed. Thus, bypassing the WHOIS check.

## OS's

Tested and confirmed working on:

* Mac OSX 10.9.1
* CentOS 6.4
* CentOS 5.10
* More to come...

If working for you (or not), please feel free to drop me a line with your OS/Environment.

## License

[MIT License](http://api.marquelmedia.net/lic/LICENSE.md)


