
![[Pasted image 20251108225420.png]]


- This was an interesting challenge and was happy to draw `first blood` on the challenge and this had many days without anyone figuring it out
- The challenge was based on `Android` phone  `data`  that was presented after downloading a `.rar` folder
- After downloading the `data.rar` folder in my `kali` box i unzipped 
  
  ![[Pasted image 20251108225752.png]]

- The folder was successfully un-archived, i then navigated to the folder to investigate it further. The sheer amount of the folder was confusing 
  
  ![[Pasted image 20251108225935.png]]

- The first idea that came to my mind was let me `grep` the flag out of these folders :)
- I stumbled upon this and thought this was the flag
  
  ![[Pasted image 20251108231218.png]]
  
- After several attempts to grep the data out of the folders , i realized i was not going anyway, and also after seeing that some of the folders inside had nothing in them a thought struct me, _what if i can arrange the folders according to size?_
- I went back to my terminal and arranged the folders to check them by size
  
  ![[Pasted image 20251108230226.png]]

- From the sizes i started from the highest in size
- After several efforts going inside the folder i stumbled on this folder `/media/0/WhatsApp/Media/WhatsApp Images`
- In the folder there were numerous images
  
  ![[Pasted image 20251108230607.png]]
- I opened my image viewer here and started checking the images, some of the images did not make sense , and _yes_ i did run `exiftool` on them to check their metadata but to no avail
- I found this image rather intruiging
  
  ![[Pasted image 20251108231404.png]]
  
  - The first attempt was think probably the `model` is samsung since i had previously seen the `galaxy` tag
  - i google the model and still this was a dead end, i did not know that i was staring at the `answer`, Did you see it ? i bet not well here
    
    ![[Pasted image 20251108231600.png]]
  - I went to google to search for an `IMEI` service to view the model
  - I stumbled upon this [website](https://www.imei.info/)
  - I entered the `IMEI` code and found this
  
    ![[Pasted image 20251108232318.png]]

- Here i got the model and this was the flag `SADC{PS5}`
- I hope you enjoyed