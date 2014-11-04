This is a small script to grab the required bungie cookies, this enables you to query the 'protected' API calls.

```
import requests

method = "XBL"

if method == "XBL":
    url = "http://www.bungie.net/en/User/SignIn/Wlid?bru=%252fen%252f"
    payload = {
        "username" : xbl_email,
        "passwd" : xbl_pass
    }
elif method == "FACEBOOK":
    url = "http://www.bungie.net/en/User/SignIn/Facebook?bru=%252fen%252f"
    payload = {
        "email" : fb_email,
        "pass" : fb_pass
    }

with requests.session() as s:
    response = s.get(url)

    if response.history:
        print "Request was redirected"

        for resp in response.history:
            print resp.status_code, resp.url
        print response.status_code, response.url

        response_post = s.post(response.url, payload)

        for resp in response_post.history:
            print resp.status_code, resp.url

        #text_file = open("output.html", "w")
        #text_file.write(response_post.text)
        #text_file.close()

        print response_post.headers['set-cookie']
        print response_post.headers["content-length"]

        for c in response_post.cookies:
            print c

        print response_post.cookies["bungleatk"]
        #for c in response_post.cookies:
        #    print c.

    else:
        print "Redirect did not work"
```
