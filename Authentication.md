Authentication
=

Get the redirect URL
=

Call one of the following URL's to get a valid redirect to the network you want:

**Xbox Live**  
http://www.bungie.net/en/User/SignIn/Wlid?bru=%252fen%252f

**PSN**  
http://www.bungie.net/en/User/SignIn/Psnid?bru=%252fen%252f

**Facebook**  
http://www.bungie.net/en/User/SignIn/Facebook?bru=%252fen%252f

These URLs will redirect you to the appropriate login screen.

Perform headless login
=

A scripting language can be used to login to your favorite OAuth site and let it be returned to the bungie site.

Grab the right tokens
=

When you get redirected back to the Bungie site, it will set a couple of cookies for you. We need to grab those to get to the private API queries