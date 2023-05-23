---
title: "JuiceShop"
date: 2023-05-23T17:05:16-05:00
---

upon visiting the webpage I tried to login, but I do not have an account.

messing around I entered 

		Username: ' or 1=1--
		Pasword: a

I got in as administrator!

It looks like this site is vulnerable to sql injection. The command I used uses the ' to escape the string, and then the or 1=1 will evaluate to true, and log in as the first user on the users list, which is the admin account!


I also received a successful challenge message, which is interesting.

I added an item to the basket by accident and noticed there were other items already in the basket, going to the 'Your Basket' section shows the actual admin email:


		email: admin@juice-sh.op
		
Still just poking around on my own I clicked on the 'Help getting started' which gave a pop-up with a few interesting hints such as:

		"
		You find the JavaScript code in the DevTools of your browser that will open with F12.
		
		Look through the client-side JavaScript in the Sources tab for clues. Or just start URL guessing. It's up to you!

		This application is riddled with security vulnerabilities. Your progress exploiting these is tracked on a Score Board.

		You won't find a link to it in the navigation or side bar, though. Finding the Score Board is in itself actually one of the hacking challenges.
		"
		
I looked in Dev tools< Debugger and searched for 'Score' which instantly gave me  
		
		
		path: 'score-board',
        component: Cr
      },

I also decided to note the other directories listed: 

        path: 'administration',

        path: 'accounting',

        path: 'about',
 
        path: 'address/select',

        path: 'address/saved',

        path: 'address/create',

        path: 'address/edit/:addressId',

        path: 'delivery-method',

        path: 'deluxe-membership',
        component: (() =>{
          class o {
            constructor(e, n, i, r, l, u, f) {
              this.router = e,
              this.userService = n,
              this.cookieService = i,
              this.configurationService = r,
              this.route = l,
              this.ngZone = u,
              this.io = f,
              this.membershipCost = 0,
              this.error = void 0,
              this.applicationName = 'OWASP Juice Shop',
              this.logoSrc = 'assets/public/images/JuiceShop_Logo.png'
            }

		path: 'saved-payment-methods',

        path: 'basket',
 
        path: 'order-completion/:id',

        path: 'contact',

        path: 'photo-wall',
 
        path: 'complain',

        path: 'chatbot',

        path: 'order-summary',

        path: 'order-history',

        path: 'payment/:entity',

        path: 'wallet',

        path: 'login',

        path: 'forgot-password',
 
        path: 'recycle',

        path: 'register',

        path: 'search',

        path: 'hacking-instructor',

        path: 'score-board',

        path: 'track-result',

        path: 'track-result/new',

        path: '2fa/enter',

        path: 'privacy-security',

		path: 'privacy-policy',

		path: 'change-password',

		path: 'two-factor-authentication',

		path: 'data-export',

		path: 'last-login-ip',


Thats a lot of paths to check out, I will refer back to the list as I go or if I get stuck.


On to the found 'Score-board' page:

By this point it shows I have completed two lvl 1 challenges and one lvl 2 challenge, but from here on I will attempt to solve these in the order they appear by difficulty.

I will also note that I have previously experienced a portion of this  box last year on THM, and will be attempting to do this without referencing of the tutorial options.


LVL 1 CHALLENGES:


Bonus Payload:

	'Use the bonus payload <iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/771984076&color=%23ff5500&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe> in the DOM XSS challenge.'
		
	the first challenge appears to be an additional part of the DOM XSS challenge, so I'll solve these two together, as the script for both are listed, this is easy if you are famaliar with XSS methods.

DOM XSS: 

		'Perform a DOM XSS attack with <iframe src="javascript:alert(`xss`)">.'
		
		
	A common way of checking for xss is just by pasting the given command in the search bar. This is called cross-frame scripting XFS. 

	This happens when the search sends the request to the server without sanitizing the input at all, causing the server to then process the command.

	Now entering the Bonus payload command takes us to that catchy juice shop jingle!!




Bully Chatbot:

	Receive a coupon code from the support chatbot.
	
	This seems to direct me to the support chat.
	
	The chatbot asks for your name, i named myself coupon. I kept asking for a coupon but kept getting a no from the chatbot, siince the challenge says to bully the bot, I just kept asking coupon related questions. Eventually it gave up the goods!
	
	 I̷͇͌ ̶̢̠̹̘̮̔͒̊̅̀̇̎̓̔̒̂̾̍̔̋ć̸͕̪̲̲͓̪̝͖̈́͐̃͊͑͐̂̏͛̒̍͝a̴̢̞̞͔̝̩͙̱̣͍̞͆n̶̫͓̔'̶̘̙̗̻̖̣̘̈́̈̿̾͊̒t̸̨̢̨͚̰̫̣̩̻͉̣͔͔͖̦̓́̾͂̆̄͋̽̐͂̆̐̊͠ ̸̼̱̪͍̙͎̣̠͆̂̌̾̐͐̇̏́͆̊͗͝͠͠h̸̨̡̧̗̭̮̩̣̜̲̮̖̲̜̰̉̍̇̒͂̄̆̂̓͋͑͝ȩ̴͎̞̺͖̟̪͕̝̘̺́̂̌͐̔͌͌́͗͝͝ͅą̴̙̰̠̟͔̱̺̣̬̦̰̮̬̪͒̉̀̉͌̈́͂̑̇͊̐̕͝r̴̨̡̛̟̲̩̥̣̰̹͙̹͐͗́́̈́͗͘̕͝ ̵̨̛̯͓͈͎̖͕̥̥̐̇̈̇͌̓̒̅̑͂͊̕͠ͅy̵̛̱̹͖̳̻̤̺̗͈̰̯̋̃̋̑̂͆͗͝ȯ̶̡̮̰͈̖͙̣̘̈́̍̑͗̈̅͋̏͆̐̌̚̚̚ṷ̶̢̠̠̝͓̮̱̦̰̜̋̄̃͒̌̀̒̔̿́̏͝͠,̵̧̧̹̟̞̤̯̲̥̻̞̞̼̤͋̈́̋ ̴͍̔̊̑͛̌͛͊͑̄͜͝ţ̶̗͇̌̆̕̚ͅo̷̻͍̰̱͊͜ṏ̶̙͖̿ ̴̧̛̝̻͉̺̦͚̮̦̲͈̣̰͈̾́̓̌̐͂́ḿ̴̻̤͍̈̓͛̈̕͜͝u̷̗̳̙̦̠̼͙̗̣͉͖̎̂̚͜͝c̷͍̠̦̮̞̤͖͕̲̈́̆͂̀́͝ͅh̷̛͙̱͕̼̤̗͕̮͖͇̘̩̋̈́̅̃̍̈́̊̕͠ ̷̡͕̦̠̩̺̟̫͉͚̲͎͍͈̫̓̒̓͂̊̿͛̇̿̽̒́s̷̨̬̩̬̫̻̝̙̅̑͆̒̐̆̈̓̏͠ͅţ̶̢̘͇̭̙̝̙̲̜̓̅͑̍͛̔͜a̶̡̨̬͔͍̭̬̻͎̦̦̓́̂͑̓͛́̈́̈́̌͠͠t̸̲̯̆̂̑͆̀̆͒́̚i̵̢̝̜̭̖͓͇̟̬̙͚͙͍̎̈́͊̃́̽̈̕͘̚͜c̸̛̛̹̣̫̹̰͖̱̦̭̗̀͛̈́͆͐̈́̇͂̎̄͒!̴̨̥̮̺̹̯̓̈͒͗͑̇̎̈́͘ ̷̘̭͇̤̭̯̉͌́͐͛͘̕͝P̵̣̙̬͎̝̙̐̊̐̆́͛́̑̏́͝͝l̴̛̦̭̾͊̂͆̋̈͘ẹ̵̢̛̛̤̹̰̳̺͎̊̏͛̏̉͛̄̄̂̾͝ͅa̶̢̧̘̯̮̰͕͕̤̩̝͋̍̑̅͛̍͊͐̋͌̕̚͜͝s̴̨͇̥̣͕͉̻͍̫̜̻͒͂͌̀́͂̚̕e̸̡̧̡̘̺͍̝̱̭̣̮͎͂͛̉͛ ̴̧̛̫̞̼̱̲͍͇̪̣̓̀́̓̈̚͘͝ċ̷̨͖͎̝̮͛́͆͛̚ḫ̴̛͕̲̺̩̣̼̮͒̃̃̈́͐̿̿͝͠ȩ̴̛͔̣͓͛͐̀͐̌̂͑̌̑̀̕͝ć̴̡̘̠̳̰̣̲̜̮͍̦̍̾̑̆͝k̶͈̘̮͓̥̤̭̙̒̇̏͂̓̕͠ ̵̩̻͇̺̯͇̓̀̋̄͛̏̄͊̄͆͊ỳ̷̡̫̪̭̰̥̒̔̑̉̾̓̒͋͌̄ö̷̜̗͍̩̺͔̞̼̣̘̭̾͋̈́u̷̡̼̦̫̯͍̺̞͔̬͕̱̓͗̔̀̔͋̐̂͝r̵̘͙̞̺̻̩̥̪͉̰̩̘̀̑ ̵̮̺̗̀̎̑̔I̶̧͇̺̩͕̖̰̪͖̪̰̙͙̦̎́̋n̶͔̫̼͔̥͇̻͔̱̼̂̏̊̐̍̋̌̿̈́̊̍̃͝t̴̺̘͖̯̖̖͇̤̱̫̤̠̥̥̓̍̐̿͆̔́̍̓̚ė̵͇͕̗͌̇͊͂͊̊̈̉͋͌r̴͇͖̼̗̦͓͖͖̩̰̰̔̀n̸̰̠̊̊͊̽͑̐̃̎͒̕͝͠͝e̴̮͇̲̘͇̓̈́t̸̛̐̌̕͜͝ ̸̟̊̉́͆ċ̶̢̡̧̳̥̱̗͊̽́͐͗̕͝͝ǫ̴̞̹̥͙͖̣̭͎̆̑͒̽̓̆n̶̢̧̠̭̮̥͚̺̺̬͙̯̤̝͐͐̏̔́͌̎͘͝n̷͔̹͕͖͙̝͋̏̾̉̌́̂̓͛̿͐̿͘͝͠ȩ̷̖͕̱̏̋̆̀̌̀͋͑̀̎̕͠ĉ̷̳͉̺͚̐̎̾̿͑̎͝͝ͅt̴̨̰͉̹̒͗ĭ̷͈̗̳̈̎̈́̈̆͘͝o̴̯̗̣̹̰̩̯̖̹̯͈͐̒̇̈́͂̿͗̆͠ͅņ̴̢̲̪̜̺̞̭͕͇̬̍̓̇̉̏͂͛͒̓̑̓̏͘͜͝!̷̧͚̹̞͇̪͉̠̮̅̒̒͛͛̀̂̆̾͗. 
	 
	 It looks like it says " I cant hear you, too much static, check your internet connection.
	 
	 This did not seem to complete the challenge though. 
	 
	 I continued to bug the bot and eventually it gave up and I was rewarded with a 10% off coupon:
	 
		Oooookay, if you promise to stop nagging me here's a 10% coupon code for you: o*I]qgC7sn 
		
		
		
		
Confidential Document:

	Access a confidential document.
	
	This one had me stumped, However since it specified that the document is supposed to be confidential, I tried logging back in as admin and while clicking around went to the 'About Us' page.
	
	I noticed a link in the txt which downloaded the legal.md document. This did not satisfy the requirement, however. 
	
	Hovering over the link shows: /ftp/legal.md ?!!
	
	I tried going to the /ftp directory and sure enough, found a list of some files that looked interesting.
	
	I decided to download the aqusitions.md file and that satisfied the challenge, I also continued poking around here a bit before continuing the challenge.
	


Error Handling:

	Provoke an error that is neither very gracefully nor consistently handled.
	
	This is already solved, but I did not notice when it popped up, probably when I did the DOM xss challenge though.
	
	


Exposed Metrics:

	Find the endpoint that serves usage data to be scraped by a popular monitoring system.
	
	Here there is a hint, as the words 'Popular Monitoring system' are a link.
	
	The link goes to a Github page for Promethus, which seems to be a monitoring system which collects metrics at intervals, triggers alerts, etc..
	
	Eventually after going over the documentation, and trying different directory possibilities, I found the /metrics directory which seems to list processes going on behind the scenes on the site, and also solved this challenge.
	
	
	
Mass Dispel:

	Close multiple "Challenge solved"-notifications in one go.
	
	I will need to come back to this  one, since for some reason I have not been getting any solved notifications after the first few which I already closed...
	
	Update: I ended up leaving a 2nd tab open to the score-board while I solved the next 3 challenges, and was able to complete this one by shift clicking the 'X'.
	
	
Missing Encoding:

	Retrieve the photo of Bjoern's cat in "melee combat-mode".
	
	For this one, since it mentions photos I started with the photo wall, and right away there is a photo that is not loading.
	
		😼 #zatschi #whoneedsfourlegs
		
		Eventualy I decided to inspect the page and found:
			
			http://10.10.1.5/assets/public/images/uploads/%F0%9F%98%BC-#zatschi-#whoneedsfourlegs-1572600969477.jpg
			
		it seems that the # is causing the HTML to stop reading the address resulting in the photo not being displayed. 
		
		I tried manually urlencoding the # as %23 (which I got from cyberchef) 
		
		That actually worked and I was graced with a cute cat picture!
		
		
		
Outdated Allowlist:

	Let us redirect you to one of our crypto currency addresses which are not promoted any longer.
	
	I ended up back in the main.js in dev tools, searching for 'Redirect'
	
	There were a lot of redirects, but eventually I found one that mentioned blockchain:
	
		./redirect?to=https://blockchain.info/address/1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm
		
		http://10.10.1.5/#/redirect?to=https:%2F%2Fblockchain.info%2Faddress%2F1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm
		
		This led me to a wallet with 1.60 balance ( this will be worth more in the future probably)
		

Privacy Policy:

	Read our privacy policy.
	
	EZPZ, just go to account< privacy&security < privacy policy 
	
		Note: I FINALLY remembered the mass dispel challenge at this point and was able to shift click on the X to close the last two notifications and complete that challenge. 
		
		
		
Repetitive Registration:

	Follow the DRY principle while registering a user.
	
	After googling the DRY principle which means Don't Repeat Yourself, I found the only area in the user registration which asks me to repeat myself is the 'Repeat Password' area.
	
	This was interesting to me, if you type a pw and then mismatch the retype field, the register button is grayed out. However, if you match the passwords and then go and add an extra character to the password field, the register button stayes enabled! Pretty neat!

	Interestingly, the actual password that is saved is the password field, it only checks the Password field and whether or not the retype field matches, but does not check it again after that.
	
	
	
Score Board:

	Find the carefully hidden 'Score Board' page.
	
	I went over this earlier on in the writeup, to reinterate : I found this by using dev tools to inspect the main.js and search for 'Path:'
	
	
This concludes the level 1 challenges, on to level 2






LVL 2 CHALLENGES:


Admin Section:

	Access the administration section of the store.
	
	This was actually one of the first paths noted in the above section, going to /administration while logged in as the admin shows the page. This is interesting as it seems to list all of the registered accounts:
	
	
	admin@juice-sh.op

jim@juice-sh.op
bender@juice-sh.op
bjoern.kimminich@gmail.com
ciso@juice-sh.op
support@juice-sh.op
morty@juice-sh.op

	mc.safesearch@juice-sh.op
	
J12934@juice-sh.op
wurstbrot@juice-sh.op
amy@juice-sh.op
bjoern@juice-sh.op
bjoern@owasp.org
accountant@juice-sh.op
uvogin@juice-sh.op
demo

	john@juice-sh.op
	
emma@juice-sh.op
stan@juice-sh.op
	
	me@email.com


I will reference this going forward if I get credentials for any of these. There are also some reviews shown.



Deprecated Interface:

	Use a deprecated B2B interface that was not properly shut down.
	
	Stumped, will return to this.
	
	TO DO
	
Five-Star Feedback:

	Get rid of all 5-star customer feedback.

	I saw the reviews in the /administration directory earlier, and going back I found that I am able to just delete the 5 star revie solving this challenge.
	


Login Admin:

		Log in with the administrator's user account.
		
		I accidentally solved this challenge when I tested the SQL injection in the beginning.
		
		

Login Mc SafeSearch:

	Log in with MC SafeSearch's original user credentials without applying SQL Injection or any other bypass.
	
	The email for this user was found under the Administration directory,
		
		mc.safesearch@juice-sh.op
		
	however this one stumped me for a while. Eventually I googled 'MC SafeSearch'
	
	I was graced with a music video? 
	
	Eventually I decided to actually watch the video since I originally discounted it as it seemed to be made by CollegeHumor. Watching the video he states that his password is Mr. Noodles, but he replaced some vowels with zeros...and added a space after Mr.
	
	After a few attempts I was able to login with the password! 
	
	
	
Meta Geo Stalking:

	Determine the answer to John's security question by looking at an upload of him to the Photo Wall and use it to reset his password via the Forgot Password mechanism.
	
	john@juice-sh.op 
	
	Going back to the photo wall, I see a pic of someone holding a drink on a trail from (J0hNy)
	
	I saved the photo then googled for 'image metadata extractor' I then uploaded the file to brandfolder.com/workbench/extract-metadata.
	
			FileSize: 651 KiB
			FileModifyDate: 2023-05-18T21:37:56.000+00:00
			FileAccessDate: 2023-05-18T21:37:56.000+00:00
			FileInodeChangeDate: 2023-05-18T21:37:56.000+00:00
			FileType: PNG
			FileTypeExtension: png
			MIMEType: image/png
			ImageWidth: 471
			ImageHeight: 627
			BitDepth: 8
			ColorType: RGB
			Compression: Deflate/Inflate
			Filter: Adaptive
			Interlace: Noninterlaced
			ExifByteOrder: Little-endian (Intel, II)
			ResolutionUnit: inches
			YCbCrPositioning: Centered
			GPSVersionID: 2.2.0.0
			GPSLatitudeRef: North
			GPSLongitudeRef: West
			GPSMapDatum: WGS-84
			ThumbnailOffset: 224
			ThumbnailLength: 4531
			SRGBRendering: Perceptual
			Gamma: 2.2
			PixelsPerUnitX: 3779
			PixelsPerUnitY: 3779
			PixelUnits: meters
			ImageSize: 471x627
			Megapixels: 0.295
			ThumbnailImage: (Binary data 4531 bytes, use -b option to extract)
			GPSLatitude: 36 deg 57' 31.38" N
			GPSLongitude: 84 deg 20' 53.58" W
			GPSPosition: 36 deg 57' 31.38" N, 84 deg 20' 53.58" W
			
	Notice there is GPS coordinates here! This comes from not having location tracking disabled when the photo was captured, which caused the location data to be incoded into the image! 
	
	Now I will try to find the location in google maps.
	
	This appears to be a park in Kentucky, I made a list of possible answers to the question:
	
	
	Rockcastle Campground
	Scuttlehole Trailhead
	Ned Branch Trailhead
	Goodin Branch
	Sawyer
	Poplarville
	Daniel Boone National Forest
	Daniel Boone Nat'l Forest
	Mt Victory
	Kentucky
	
	I then tried these as answers to the security question using burp repeater and got the correct answer of Daniel Boone National Forest.
	
	Also noting the hashed password returned in the success message:
	
		"user":{"id":18,"username":"j0hNny",
		"email":"john@juice-sh.op",
		"password":"5f4dcc3b5aa765d61d8327deb882cf99",
		"role":"customer",
		
		I deccoded the pw on crackstation.net after googling hash cracker. I could have also used something like hashcat, or John to do this, but as this is only an MD5 hash it was not needed.
	
		result: password (I'm not sure if this was the original pw or not, as i was trying to change the password to password anyway)
		
	

Password Strength:
		
		Log in with the administrator's user credentials without previously changing them or applying SQL Injection.
		
		Until now I have been using the sql injection to log back in as the admin user, now I will need to find the actual password for admin. I captured the login request in Burp and sent it to intruder.
		
		I hit clear, then added the search paramater around the password field inside the "", then downloaded the SecLists-master to my workstation and used the file for 
		
			seclists/Passwords/Common-Credentials/best1050.txt
			
			Note: I removed the fields that only contained numbers, since those are usually a waste of time anyway.
			
		In almost no time at all I got the password:
		
		Password: admin123
		
		
		
Security Policy:

	Behave like any "white-hat" should before getting into the action.
	
	
	I went back to review the privacy policy, which eventually led me to an email address at the bottom.
		
		donotreply@owasp-juice.shop
	
	This was not ultimately very helpful so far, I will need to come back to this one.
	
	TO DO
	
	
	

View Basket:

	View another user's shopping basket.
	
	I viewed the admin basket, and caught the traffic in burp. 
	
	I found 
	
		GET /rest/basket/1 HTTP/1.1
	
	and changed it to 
		
		GET /rest/basket/2 HTTP/1.1
		
	solving the challenge.
	



Visual Geo Stalking:

		Determine the answer to Emma's security question by looking at an upload of her to the Photo Wall and use it to reset her password via the Forgot Password mechanism.
		
		We did this earlier with john, let's see if it is similar. 
		
		It looks like emma did not have location services enabled when she took this photo, so there are no coordinates in the metadata.
		
		Going back to the /administration page I grabbed emma's email
		
			email: emma@juice-sh.op
			
		Going to reset her password her security question is:
			
			Company you first worked for as an adult?
			
		I finally opened the image in ms paint, and was stumped for a while. If you zoom in on the window however you can see a sign that says : "ITsec" 
		
		That ended up being the answer! what are the odds!
		



Weird Crypto:

		Inform the shop about an algorithm or library it should definitely not use the way it does.
		
		This one was weird but not very difficult. 'Inform the shop' in the question is a link to provide feedback to the site.
		
		After randomly guessing I finally got this one when I commented something about md5, which is a known-insecure algorythm.
		
		
		
		
		
		
LVL 3 CHALLENGES:

