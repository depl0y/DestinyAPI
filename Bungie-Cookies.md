This is a small script to grab the required bungie cookies, this enables you to query the 'protected' API calls.

```
bungled = ""
bungledid = ""

import requests

def check_cookies(url, cookies):

    if "bungled" in cookies:
        global bungled
        bungled = cookies["bungled"]

    if "bungledid" in cookies:
        global bungledid
        bungledid = cookies["bungledid"]

method = "FACEBOOK"

if method == "XBL":
    url = "https://www.bungie.net/en/User/SignIn/Wlid?bru=%252fen%252f"
    payload = {
        "username" : xbl_email,
        "passwd" : xbl_pass
    }
elif method == "FACEBOOK":
    url = "https://www.bungie.net/en/User/SignIn/Facebook?bru=%252fen%252f"
    payload = {
        "email" : fb_email,
        "pass" : fb_pass
    }

with requests.session() as s:
    response = s.get(url)

    if response.history:
        print response.status_code, url

        check_cookies(url, response.cookies)

        for resp in response.history:
            check_cookies(resp.url, resp.cookies)

        response_post = s.post(response.url, payload)

        check_cookies(response_post.url, response_post.cookies)

        for resp in response_post.history:
            check_cookies(resp.url, resp.cookies)

        headers = {
            "User-Agent" : "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10) AppleWebKit/600.1.25 (KHTML, like Gecko) Version/8.0 Safari/600.1.25",
            "X-Requested-With" : "XMLHttpRequest",
            "X-API-Key" : "10E792629C2A47E19356B8A79EEFA640",
            "Accept-Language" : "en-us",
            "x-csrf" : bungled
        }

        vendor_response = s.get("https://www.bungie.net/Platform/Destiny/1/MyAccount/Character/2305843009244775435/Vendor/1575820975", headers = headers)

        print vendor_response.text

    else:
        print "Redirect did not work"
```