---
title: Messing With Scammers
date: 2022-01-05
---

### Who Doesn't Hate Scammers?

We all hate scammers. I think that's a fairly non-controversial statement. So imagine my elation when I got a scam email in my mailbox ready to be exploited. 

Right up front, this post is heavily inspired by Engineer Man's [awesome video](https://www.youtube.com/watch?v=UtNYzv8gLbs). The guy is an absolute legend at what he does and is a ton of fun to watch and learn from. Highly recommend checking out his [content](https://www.youtube.com/c/EngineerMan).

#### Messing With the Scammer

So, I received this email from "Geico" claiming to confirm my desire to unsubscribe from their marketing emails. Following the link on the main page led me to a page that looked like:

![](/images/scam-form.png)

Note: using [Tor](https://www.torproject.org/) as to not give the scammers any personal identification like my browser user-agent or ip.

Like the Engineer Man video, my goal was to construct a bunch of fake emails, and then programmatically send each one to the scammer's sever. The idea being: if I could send thousands of emails over, the scammers would have a hard time telling legitimate emails from my fake ones. 

#### Inspecting the Network Request

Sending over some test data and and inspecting the network data revealed that the browser was indeed sending a standard POST request to:

![](/images/post-url.png)

Looking at the headers I could see the only two I cared about:

![](/images/ct-header.png)
![](/images/auth-header.png)

With this information, I knew I could replicate the request using python.

#### Duplicating the Request

I could have spent the 30 minutes building a python program that would replicate the POST request, but instead I remembered a quick trick I learned about last year.

In the network tab, I clicked on the network request, and selected "copy as cURL":

![](/images/copy-curl.png)

Then, using this wonderful [site](https://curlconverter.com/), I was able to automatically convert the cURL command to a python program. Saved a bit of time :)

Finally, I went to a email generator website, downloaded 5000 fake emails, and saved them in `fake_emails.csv`.

Adding in a loop to loop over the fake emails I ended up with:
```python
#file: fuckscammers.py
import requests
import time

headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; rv:91.0) Gecko/20100101 Firefox/91.0',
    'Accept': 'application/json, text/plain, */*',
    'Accept-Language': 'en-US,en;q=0.5',
    'Referer': 'https://www.ninehatten.com/',
    'Content-Type': 'application/json',
    'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0eXBlIjoib3B0b3V0IiwiY2FtcGFpZ25faWQiOjE3NzIwMywibWFpbGVyX2lkIjoxMTA4NTEsImNtYV9pZCI6MzAwMzUzMjEsImlhdCI6MTY0MTM5NTQzNiwiZXhwIjoxNjQzMjA5ODM2fQ.n-o3p4N-gdNOtwMAiq9qss3c69Sya4veoya9gSXqIV8',
    'Origin': 'https://www.ninehatten.com',
    'Connection': 'keep-alive',
    'Sec-Fetch-Dest': 'empty',
    'Sec-Fetch-Mode': 'cors',
    'Sec-Fetch-Site': 'cross-site',
    'TE': 'trailers',
}
count = 1

for email_address in open("fake_emails.csv").readlines():
    print(count)
    count += 1
    data = '{"email":"' + email_address.strip() + '","preference":[],"wasRedirectedToAds":false}'
    response = requests.post('https://api.optoutsystem.com/campaigns/177203/optout-emails', headers=headers, data=data)
    print(response.status_code)
    time.sleep(1)
```

#### Running on Remote Server

Obviously I don't want to make these requests from my personal machine, so I quickly spun up a Droplet on [Digital Ocean's](https://www.digitalocean.com/) platform.

I spun up the lowest tier of droplet and set the preferences to:

![](/images/droplet-location.png)
![](/images/droplet-name.png)

#### Putting it all Together

Running my file with a simple `python3 fuckscammers.py` and letting it sit, I got back successive 204 responses indicating that the scammer's server was accepting my POST requests and my fake data was saved. With any luck this will inconvenience or setback the scammer as they have to sort through a slog of fake data. Or at least, hopefully it eats up more of their precious time than I spent. 

Thank you for reading!