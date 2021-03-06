# Vishwa CTF Writeup
## Reverse Engineering 

### Apollo11

Challenge Description:

Apollo's next mission is put on hold owing to a backdoor passkey. I'm pretty sure some rival countries have a hand in this. Hope you find it...

Solution:

Got the flag directly using strings command on that iso file.
$ strings Apollo11.iso | grep "vishwaCTF"

flag: **vishwaCTF{I50_1s_A_MEs5}**


### Rotations

Challenge Description:

Rotations make you dizzy...don't they?

Solution:

We are given a file,by giving permission and running it.We can see that if we give the correct input it will give us flag.
By using gdb and debugging the program in the main function we can see memcmp statement by setting breakpoint at that place and check to which string it is being compared.
The string is ``JIHGFEDCBAAAAAA``
By entering this string we get ``ivfujnPGS{s1Nt_1f_e0g4gRq_Ol_!3}``
Looking at the challenge name i used rot 13 which gave the flag 

flag: **vishwaCTF{f1Ag_1s_r0t4tEd_By_!3}**

### Give it to get it

Challenge Description:

vishwaCTF{f14g_1s_Wh3r3_Th3_h3aRt_L1Es} HEHE THIS Ain't the flag. You'll have to give it something so that it spits out this flag. The "something" is the flag.

Solution:

From the description i understood that we have to give something so that ‘vishwaCTF{f14g_1s_Wh3r3_Th3_h3aRt_L1Es}’ gets printed. When i tried to check the code using ide , i understood that it basically converts a hex value to its corresponding ASCII value. So i converted that given flag to hex(7669736877614354467b663134675f31735f57683372335f5468335f68336152745f4c3145737d7d)  and gave that hex value as input .  

flag: **7669736877614354467b663134675f31735f57683372335f5468335f68336152745f4c3145737d7d**


### Misleading Steps

Challenge Description:

Misleading Steps often lead you to unexpected places...

Solution:

when we open the file in gdb, we see some characters are moved to offsets starting from [rbp-0xb0] to [rbp-0xc] 
concatenating and printing all characters, we get the flag 

$ gdb> x/sw $rbp-0xb0

flag: **vishwaCTF{UmM_w3iRDooo0_1_Am_th3_r34l_0n3}**

### Facile

Challenge Description:

Mr Bingo has hidden something secretive inside...

Solution:

From the extension we get to know it is a compressed file,when we extract using `binwalk`, we get a zip and a file, when we do `strings` on the file, we get the flag

$ strings FOLDER_ITEM | grep -i "vishwactf"

flag: **vishwaCTF{r3v_1t_1s5s5s}**

### Suisse

Challenge Description:

Let's Uno His Name and reduce 3 from each uno you found. Admin suffers from cardiovASCIIular disorders. So do obtain the flag accordingly.

Note: Do not include whitespaces in the flag if you find any, and your flag should be of the format vishwaCTF{flagtext}.

Solution:

when opened the elf in IDA,Inside `_flag(void)`,we find some characters, Using the hint in description and subtracting each character by `3` and concatenating them, we obtain the flag 

$ python -c 'print("".join(chr(ord(i)-3) for i in "oXkQq]4v8hfXUh"))'

flag: **vishwaCTF{lUhNnZ1s5ecURe}**

### FlowRev

Challenge Description:

The name of the challenge signifies the method of solving.

Solution:

Analysing the code we find that there is `test` instruction for value in [rbp-0xc], which was initialized to zero, when the test happens with value in [rbp-0xc] as zero the program quits, else it enters a loop
we can overwrite the value inside [rbp-0xc] since the program uses `gets` 
The loop prints `433` integers taken starting from the offset [rbp-0x280]

we here have a hint `4+3+3-2 conversion required`,which says `octal conversion required`
From which we can conclude that the printed values are in base 8

considering the first `140`  values from the output printed (from then the values are grater than `177`) and converting each number to octal and concatenating we get a hex string which when converted to text gives the flag

```
array = [67,66,40,66,71,40,67,63,40,66,70,40,67,67,40,66,61,40,64,63,40,65,64,40,64,66,40,67,142,40,65,65,40,65,146,40,64,144,40,63,64,40,66,145,40,66,61,40,64,67,40,66,65,40,64,64,40,65,146,40,67,64,40,63,60,40,65,146,40,66,144,40,63,60,40,64,64,40,63,61,40,66,66,40,65,71,40,65,71,40,65,71,40,65,146,40,65,67,40,63,63,40,66,143,40,66,143,40,65,146,40,66,64,40,63,63,40,67,63,40,66,65,40,67,62,40,65,143,40,62,146,40,63,63,40,66,64,40,67,144]

flag = "".join(chr(int(str(i),8)) for i in array) 
flag = "".join(flag.split()).decode('hex') #remove spaces and convert to hex
print(flag)
```

Flag: **`vishwaCTF{U_M4naGeD_t0_m0D1fYYY_W3ll_d3ser\/3d}`**


## GENERAL
### Prison Break

Challenge Desc:

Please help yourself, Get out of the prison! and YES, every move matters. https://prisonbreak.vishwactf.com/

Solution:
Guessed all the possible logical answers , after few attempts I got the flag.

flag: **vishwaCTF{G@mE_0f_DeC1$ions}**

### BiGh Issue 
----------

``general``

challenge desc : 

Our team recently faced a very big issue while making the frontpage website for vishwaCTF'21. Thankfully, it got resolved later and we closed the discussion off. But I guess someone accidentally posted a flag there, and had to take a lot of hearing from our guide.


solution :

In this challenge we have to go to the github page of the vishwactfwebsite'21   repo  there in the issue tab ther is  huge isse reference when we go to that issue we can see some conversation ,and there are some edited conversation when we go through that we can see that flag was deleter from the coversion of some person 
and thats the flag

flag : **vishwaCTF{bh41yy4_g1thub_0P}**

### Pub
---

``general``

In this challenge we are given a apk which shows a list of movies of avengers  and there was a hint "morese code is the way forward"

solution :
 
 when we look through that list of movies we can one movie name is external_packages and since the challenge name was pub i searched for external_packages in pub.dev and found it's [github repo](https://github.com/anilChouhan-sh/external_package) and continued searching beacause the readme said "Get your vishwaCTF flag here". Found a lead in  [pubspec.yaml](https://github.com/anilChouhan-sh/external_package/commit/6e2260c9fff93d396f3b62de5e010e7eca1d4453) file's recent commit.
 
 ```fix
 pubpubpubspec pubpub pubpubpub pubpubpubpub pubspecspec pubspec specpubspecpub spec pubpubspecpub{pubpubspec pubpubpub pubpubpubspecspec pubpubspecpub pubpubspec pubspecspecspecspec pubpubspecspecpubspec pubpubspecpub pubspecspecspecspec pubpubspec spec spec pubpubpubspecspec pubspecpub pubpubspecspecpubspec pubspecspecpub pubspecspecpubspecpub specpubspecpub specpubspec pubspec specspecpub pub}
 ```
we can replace 'pub' as '.' aand 'spec' as '-' so we got 


```fix
.--.  ..-  -...  .--.  ..-  -...  ...  .--.  .  -.-.   .--.  ..-  -...  .--.  ..-  -...  .--.  ..-  -...   .--.  ..-  -...  .--.  ..-  -...  .--.  ..-  -...  ...  .--.  .  -.-.  ...  .--.  .  -.-.   .--.  ..-  -...  .--.  ..-  -...  ...  .--.  .  -.-.  .--.  ..-  -...   .--.  ..-  -...  .--.  ..-  -...  ...  .--.  .  -.-.   .--.  ..-  -...  ...  .--.  .  -.-.  ...  .--.  .  -.-.  ...  .--.  .  -.-.  ...  .--.  .  -.-.   .--.  ..-  -...  .--.  ..-  -...  ...  .--.  .  -.-.  ...  .--.  .  -.-.  .--.  ..-  -...  ...  .--.  .  -.-.   .--.  ..-  -...  .--.  ..-  -...  ...  .--.  .  -.-.  .--.  ..-  -...   .--.  ..-  -...  ...  .--.  .  -.-.  ...  .--.  .  -.-.  ...  .--.  .  -.-.  ...  .--.  .  -.-.   .--.  ..-  -...  .--.  ..-  -...  ...  .--.  .  -.-.   ...  .--.  .  -.-.   ...  .--.  .  -.-.   .--.  ..-  -...  .--.  ..-  -...  .--.  ..-  -...  ...  .--.  .  -.-.  ...  .--.  .  -.-.   .--.  ..-  -...  ...  .--.  .  -.-.  .--.  ..-  -...   .--.  ..-  -...  .--.  ..-  -...  ...  .--.  .  -.-.  ...  .--.  .  -.-.  .--.  ..-  -...  ...  .--.  .  -.-.   .--.  ..-  -...  ...  .--.  .  -.-.  ...  .--.  .  -.-.  .--.  ..-  -...   .--.  ..-  -...  ...  .--.  .  -.-.  ...  .--.  .  -.-.  .--.  ..-  -...  ...  .--.  .  -.-.  .--.  ..-  -...   ...  .--.  .  -.-.  .--.  ..-  -...  ...  .--.  .  -.-.  .--.  ..-  -...   ...  .--.  .  -.-.  .--.  ..-  -...  ...  .--.  .  -.-.   .--.  ..-  -...  ...  .--.  .  -.-.   ...  .--.  .  -.-.  ...  .--.  .  -.-.  .--.  ..-  -...   .--.  ..-  -...
```

 so we got the morse code and we can decode it to get the flag
 
 
flag : **vishwaCTF{US3FU1_F1UTT3R_P@CKAGE}**

### findthepass
---------------

challenge desc:

You have been provided with a vm of a linux os, find the password of the root

file:
[A vbox file](https://drive.google.com/file/d/14FnXZ1DiHgCFPKQF_hlZdAUAkaxzMX4J/view?usp=sharing)

solution:
Started by opening the vbox file with VirtualBox and an OS loaded. Found a terminal in Applications/System Tools and found a wordlist in a directory this_is_what_you_need.

![wordlist](https://imgur.com/p2mmMub.png)

So, using these passwords, I realized that any password which started with "password" worked to log into root. So, went to /etc/ and found the shadow file there.

![shadow](https://imgur.com/K1NxnmV.png)

We copied the shadow file out and used john-the-ripper to find the root's password to be "password"

flag: **vishwaCTF{password}**

### Find the room
I have searched for FV5M+VH,pune,maharastra.Then by checking the images of the college.
![](https://i.imgur.com/FHnZOp0.png)

From this image the deans room number is the flag.So we can see classroom number as A 004 so the dean's room number will be A 003.

Flag : **vishwaCTF{A 003}**

### Secret service
desc : Hello.
We are looking for highly intelligent individuals. To find them, we have devised a test. There is a url hidden in the image.Find the 3 prime numbers and it will lead you on a road to find us.
Good Luck
3301

Here we are given an image. Then find the dimensions of that image. The dimensions must be multiplied. The 3 primes dimensions are 1019,911,3301. So by mutliplying these 3 primes we get 3064348009.

Flag : **vishwaCTF{www.3064348009.com}**

### Magician

We are given a link. By opening link we can words and thier position. The word changes every 20mins. So we get the flag after all words are displayed within 12hrs by checking all the words everytime it changed.

Using this shell script code, we received the flag...

```
#!/bin/bash


a=1

while [ $a -eq 1 ]
do
	curl https://magician.vishwactf.com/ | grep "<h1>" >> a.txt
	sleep 19m
done
```

Flag : **vishwaCTF{cr0nj0bs_m4k3_l1f3_s1mp13}**

### front page

desc : Cover pages or front pages of newspapers and magazines contain the biggest news stories and are designed to grab a person's attention. BTW, did you know that the internet has a front page too?

Reddit is most commonly reffered to as the internets frontpage. When we look at reddit we get a suspicious post here https://www.reddit.com/user/vishwaCTF/comments/

```
Oh, how careless of me to just drop the flag in a Reddit post! Luckily I deleted it almost immediately.
But nothing on the internet is ever completely deleted.
```
So we look at the internet archive where we got this
https://web.archive.org/web/20210226174949if_/https://www.reddit.com/user/vishwaCTF/comments/lt1gzm/could_this_be_the_flag_for_a_vishwactf_2021/
```
Well, so I'm just gonna drop the flag here, and I certainly hope no hackers get access to this. So here goes:

vishwaCTF{0$dVl_1z_kFV3g_0a3mT0graD}

But hang on, this text doesn't make sense, does it? Oh well, it is what it is I guess.

Good luck for rest of the challenes!
```
**0$dVl_1z_kFV3g_0a3mT0graD** is a vignere ciphere with key **vishwaCTF**. Solving it gave the flag 

flag : **vishwaCTF{0$iNt_1s_oFT3n_0v3rL0okeD}**

### git up and dance
We are given a zip file. First ```unzip <filename>.``` 
```grep CTF *```
![](https://i.imgur.com/jOqkhx5.png)

Now in the log file check for the latest commit which is 
```
commit acd2ccc03ddafc1c838adbb3e2d3835d7656777a
Merge: 83237fb 161e271
Author: Sohan <sohan@email.com>
Date:   Wed Mar 10 23:21:23 2021 +0530
```

Now use 

```git checkout acd2ccc03ddafc1c838adbb3e2d3835d7656777a```

```grep CTF *```

![](https://i.imgur.com/bCOk3lR.png)

Flag : **vishwaCTF{d4nc3_4nd_giitupp}**

### Good Driver Bad Driver

Description:
We are starting a new service company providing on-rent good drivers, by the name BBDrivers. We already have 3600 drivers that we have classified as Good=0, Average=1 or Bad=2 and also have their scores on particular tests. We have received 400 more applications for drivers, but reviewing them will be a loss of time and money. Can you please let me know what kind of drivers these guys are? I'll even give you the old driver's data in case you need it.

Solution:
Train a knn classifier (k=3) using sklearn library to classify the drivers into Good, Average, and Bad using the given training dataset. Using this trained model to predict the values for the testing dataset, output all the predicted values in the form of integers and feed it into the website to give the flag

Solve script:
```python
import pandas as pd
from sklearn.neighbors import KNeighborsClassifier

train = pd.read_csv('drivertrainlabeled.csv')
test = pd.read_csv('drivertestunlabeled.csv')

def convert(data):
    if "Good" in data:
        return 0
    if "Average" in data:
        return 1
    if "Bad" in data:
        return 2

train = train.drop(['Driver_ID'], 1)
train['Driving_Class'] = train['Driving_Class'].apply(convert)

train.head()

X_train = train.drop(['Driving_Class'], 1)
Y_train = train['Driving_Class']

knn = KNeighborsClassifier(n_neighbors = 3).fit(X_train, Y_train)
Y_pred = knn.predict(test)

out = "".join([str(i) for i in Y_pred])
print(out)
```

Output: 
```
1110111111011011010011121101111111111111011101100111001101110011111111101011101011111111100011110100110111111111110111111111101111111101111111111100111001010111112101111110111110111100111111111111111110100110100111111012110100111111111111111121011111111101111111111110111112111101111111111111111101111110011210111001111011100121111111111111111011111121111111101111111111111111110110111110111011102111
```

Flag: `vishwaCTF{d4t4_5c13nc3_15_n3c3554ry}`


### Treasure Hunt

desc : Instagram, Twitter and LinkedIn are the steps to Social Success. And, I'm sure I put the flag somewhere on our posts            here, but I cant remember if it was the caption or comment or retweet. Can you help me find it? Go sequentially

We were given the links to the Instagram , Twitter and LinkedIn handles of vishwaCTF and going through the Instagram posts by vishwaCTF we got the first part of the flag put in the caption of the last post ,then we noticed that caption , comment and retweet mentioned in the desc and checked all the retweets in twitter and comments on vishwaCTF posts in linkedIn . we got the part 2 of the flag from the comment section of the last linked in post and the final part from the retweet on a post in twitter (https://twitter.com/cybercellviit/status/1299671113039970305)

flag : **vishwaCTF{w31c0m3_t0_v1shw4ctf}**

## Crypto

### Weird Message
--------------

challenge desc : 

My friend sent me this file containing a damn long string. He told me to find the message to prove I'm worthy of his friendship XD. Please help me do it? Something about the length is bothering me. Also, he told me to remember this short message for our next meeting. Is this really rememberable?

solution:

Opened and the txt file in notepad and changed window size and zoom, till we could identify a readeable message.

![img](https://imgur.com/o93JjKK.png)

Realising that the flag and it's mirror image are overlapped, tried to extract the flag...
![img2](https://imgur.com/2q8rF5d.png)

flag: **vishwaCTF{pr1m35_4r3_w31rd}**

### A typical day at work
----------------------

challenge desc :

The manager at mcgronalds seemed very happy today, after a tedious day at work, he shed tears of joy and said this
“yonvkahj_on_jeyonx_jeajon”… can you tell us what he said?

solution:

Assuming it to be mono-alphabetic substitution cipher, got the plaintext by entering ``yonvkahj on jeyonx jeajon`` in [quipqiup](https://www.quipqiup.com)

### Mosha
-----

challenge desc:

My friend created a font and sent me a message, I cant quite understand it.Help me decode it. He has posted the font on a social media under the name mosha font or something.

file:

![alt text](https://i.imgur.com/1gNyoH2.jpg)

solution:

Found a [post](https://www.instagram.com/p/CMT1hi5BtyQ/) in Instagram with a username "mosha_font" with the translations.

flag: **vishwaCTF{Y0UR34M0SH4N0W}** 

### From the FUTURE
---------------

challenge desc:

Accidentally frozen, pizza-deliverer Fry wakes up 1,000 years in the future and finds himself surrounded by cyclops,robots,flying cars and crazy scientists. He is given a note but he cant understand it. Can you help him??

file :

![img](https://i.imgur.com/ypgajIt.png[/img])

solution:

Considering the challenge name, I found it was in written in Futurama Alienese script, by seaching in Google.

Then transcripted the note with this image...

![alt text](https://static.wikia.nocookie.net/enfuturama/images/d/da/740px-Alien_decoder_Futurama.svg.png/revision/latest?cb=20130805223309)

flag: **vishwaCTF{WEARENOTALONE}**


## Web

### Inspect the un-Inspected 
-------------------------

desc : Home is the only place where you can practice and frequently ask questions! maybe..?

So we have to inspect the home page for vishwactf to get the flag. Searching for some time in the home page gave us part 1,part 2 was in practice tab, and part3 was in faq.Joining the parts gave the flag.
flag : **vishwaCTF{EvEry_C0iN_ha$_3_s1Des}**

### Redeem
-------

desc : One of our seller has the flags. and it seems you don't have enough money to buy the same. The only way to get money is by redeeming the coupon code. TRY UR LUCK ! 

challenge [link](https://redeeeem.vishwactf.com/)

So when we go to the link we can see that we have to buy a flag and the price for flag is 6969 but our balance is 0

![image](https://user-images.githubusercontent.com/77448514/111109155-31a2e800-8580-11eb-916d-f2ddfd93f251.png)

So when try to buy the flag we can't.
Then we try intercepting the the request with burp and change the valueof current to 6969 and we get the flag

![image](https://user-images.githubusercontent.com/77448514/111109513-e3daaf80-8580-11eb-8a6a-60fd875d64e7.png)

flag : **vishwaCTF{@DDed_T0_C@rT_}**

### UwU
----
desc : when php, anime and robots come together. they make hell of a challenge
challenge [link](https://uwu.vishwactf.com/)

When we visit the challenge link , we will be welcomed with a video but since the word robots was mentioned in the description we checked for the /robots.txt file and it gave a hint that a directory called robots exists so we visited the /robots path and it gave us the PHP source code for the challenge , looking at the source we can see that the backend takes our input in the php_is_hard param and then run it through a regex filter which replaces the 'suzuki_harumiya' with an empty string. Finally we can see we get the flag, if our input = 'suzuki_harumiya'. So we fool the regex by using the payload 'suzukisuzuki_harumiya_harumiya' . final payload: ?php_is_hard=suzukisuzuki_harumiya_harumiya

flag : **vishwaCTF{well_this_was_a_journey}**

### Is Js Necessary? 
----------------
challenge link https://isjsnecessary.vishwactf.com/

When we go to the link, it redirect us to google.com. The challenge name is is js necessary so we disabled javascript and tried again this time we got 

![image](https://user-images.githubusercontent.com/77448514/111110307-4da78900-8582-11eb-9a1f-cf6c046e42df.png)

Brendan Eich developed javasript and searching the web gave us that he took 10 days to develop javascript. Giving 10 as the input gave the flag. Also turun on the javascript before submitting.

flag : **vishwaCTF{2ava5cr1pt_can_be_Dis@bleD}**

### bot not not bot 
---------------

desc : Ain't Much, But It's Honest Work!!!

challenge link : https://bot-not-not-bot.vishwactf.com/

Visiting the page gave us 500 hyperlinks and some of the pages had a character and and their position in the flag. So we wrote a script to vist all these pages which had `Usefull`  in them
```bash=
#!/bin/bash
for((i=1;i<=500;i++))
do
    curl https://bot-not-not-bot.vishwactf.com/page$i.html >> a.txt
done
cat a.txt | grep Useful Page > b.txt
```
find the charcters and place them in appropriate positions.

flag : **vishwaCTF{r0bot_15_t00_0P}**

### Time is an illusion 
--------------------

desc : The source should convey it all 

challenge link : https://time-is-an-illusion.vishwactf.com/

Going to the webpage there is an input box and a hyperlink to the source code

```php=
<?php
include "env.php";
set_time_limit(0);
if(isset($_GET['key'])){
    $your_input = $_GET['key'];
    if(strlen($your_input)!=5){
    die("It's five characters long, and may or may not contain numbers or characters or small letters or capital letters");
    }
    for($i=0; $i<strlen($your_input);$i++)
    {
        $let_check=$_ENV['our_input'];
        if($your_input[$i]!=$let_check[$i]){
            die("VERY VERY VERY INCORRECT");
        }
        usleep(1000000);
    }
    echo getenv('THE_THING_YOU_ARE_LOOKING_FOR');
}
?>
```
So we have to input a 5 letter word and each time the character is correct we can see a delay of 1s in the response. Taking the dealy in the response we made a python code to get the password.

```python
import os
import string
import requests
scope = string.ascii_letters+string.digits
print(scope)
payload = ""
s = requests.Session()
for char in scope:
    payload = char*5
    r = s.get("https://time-is-an-illusion.vishwactf.com/handle.php",params={"key":payload})
    print(payload)
    print(r.elapsed.total_seconds())
```
Since the delay was 1s we had to try a few times but we got the password as **KuKa9** and that gave us the flag 

flag : **`vishwaCTF{PhP_h@$_iTs_0wN_PErK$}`**

### My Awesome Youtube recommendation 
---------------------------------

desc :Hey there, I made my first Flask app which recommends youtube videos for your search. Hope you like it

link : https://yt-search.vishwactf.com/

So here they have already said that uses flask. So we try SSTI. Giving the input {{7*7}} confirmed the suspicion.and giving {{config}} revealed the flag. But since it was redirecting we could only see the flag for a few seconds and had to use burp to get it.

flag : **vishwaCTF{th3_f14g_ln_c0nflg}**

## Networking

### Commenting is the key

Challenge Description:

Silicom tried communicating with Castlene and then they made some comments about it... try to find the flag through this file

Solution: 

We are given a pcap file for analyzing it i have opened it using wireshark.I checked the packets,in the 5th packet i have the found the flag in the packet comments.
Flag: **vishwaCTF{packets_are_editable}**

### Invalid

Challenge Description: 

In the previous challenge's file, what was the ip of the person who entered the wrong credentials?

Solution

so as this questions suggests we need check the ip of user who entered wrong credentials. so basically we can find credentials in either udp or dns or http. so if we check udp-stream at stream 11 we can find text(ascii) as wrong password. which gives us the ip address

flag : **vishwaCTF{212.242.33.35}**


## Forensics

### Barcode Scanner

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/1.png?raw=true)
 - Download the Image given.

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/2.jpg?raw=true)

- Use Stegsolve and invert the colors.

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/3.png?raw=true)

- This will be the final image which u get.
- Then use `zbarimg` tool to extract text from the `Barcode`.

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/4.png?raw=true)

```sh
Flag --> vishwaCTF{5oo_3ASy}
```

### Peace

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/5.png?raw=true)

- Download the `rar` file given.
- Crack the `rar password` using `rar2john`.

```
rar2john morse.rar > ki.txt
```

- `unrar` the `rar` file using password `india`

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/6.png?raw=true)

- We will get a `morse encrypted audio` file.
- Use `morse decoder` to `decode` the content.

```sh
76 69 73 68 77 61 63 74 66 7B 37 68 33 79 5F 34 72 45 5F 46 30 72 33 66 65 37 31 6E 67 7D
```

- We will get the `hexadecimal` values.
- Decode it to get the `ASCII` text.

```sh
Flag --> vishwactf{7h3y_4rE_F0r3fe71ng}
```

### Sherlock

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/7.png?raw=true)

- Download the Image File given.

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/8.jpg?raw=true)

- From the `Magic Numbers` we shall find that the given image is actually a `png` format.
- But we get it as `jpg`.
- So `change` its `format` to `png`.
- Use `zsteg` tool to extract the hidden information.

```sh
zsteg -a decode.png
```

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/9.png?raw=true)

```sh
Flag --> vishwaCTF{@w3s0Me_sh3Rl0cK_H0m3s}
```

### Comments

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/10.png?raw=true)

- Download the given `docx` file.
- Use `cat` command with `pipe` and `grep` to see the `contents`.

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/12.png?raw=true)

```sh
Flag --> vishwaCTF{comm3nts_@r3_g00d}
```

### Bubblegum

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/13.png?raw=true)

- Download the given `Audio` File.

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/14.png?raw=true)

- Open the given audio file in `audacity`.
- Upon analysing it, we find this `0.55-1.07` which could be a hint.
- Searched for the given audio in [youtube](https://youtu.be/5x441jo1-sg ) and found out that the lyrics of `0.55-1.07` portion of this video is the flag:

```sh
Flag --> vishwaCTF{oh bubble gum dear im yours forever i would never let them take your bubblegum away}
```

### Remember

- Download the files given.

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/16.png?raw=true)

- Download the files given.
- Using `registry viewer` `analyse` the file2.
- Go through the `accounts` folder.
- In key `properties` tab we can see the `last password updated time`.

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/19.png?raw=true)

```sh
Flag --> vishwaCTF{thursday_january_10_08_24_36_2013}
```

### Recovery

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/17.png?raw=true)

- `Download` the `files` given.
- Using `registry viewer` `analyse` the file2.
- Go through the `accounts` folder.

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/21.png?raw=true)

- Under `users` we can see `shreyas account` details but we will not able see the `password hash` without uploading the `syskey` file.

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/20.png?raw=true)

- The `file1` is the `syskey` for the `file2` after uploading the `syskey` in `registry viewer` we will able to see the the `hash key` and more details in `key properties`.
- So using `samdump2` dump all the `username` and `password` `hash`.

```
samdump2 file1 file2 > hashes.txt
```

![](https://github.com/abhishekabi2002/Bi0s/blob/master/Vishwa_Ctf/Assets/23.png?raw=true)

- Created a wordlist using python script `cupp.py` with hints given in description 

`The DOB is 10 January 1993 because at the time he changed the password he is 20 yrs old.`

- Using this `python script` if we input the `name,DOB` etc we shall get all possible combinations of `password`.

```
john --wordlist=shreyas.txt --format=NT hashes.txt
```

- Password = `sayerhs_093`

```sh
Flag --> vishwaCTF{sayerhs_093}
```

### Dancing LEDs

We are given a vedio which is ordino design.

The blinking of the lights indicates the binary.

Then when black is glown is denotes 1 remaining all colors denotes 0 and earth is always 0.

So we get the binary as 

```00110100 01101001 01110000 01011010 01001010 01001000 01111010 01111000 00110100 00110001```

Now we have to convert it to ascii and we get ```4ipZJHzx41.```

Now we have to convert from base58 we get ```b1!nk3r```

Flag :- **vishwaCTF{b1!nk3r}**


