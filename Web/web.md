# Web exploitation 

## Bookmarklet

![image](https://github.com/j10nelop/m3d1r/assets/152776722/8d825340-782c-4b14-9c5c-69f15e85d46b)

- open the website we seem it's have the javascript code may be is the decryption the flag

![image](https://github.com/j10nelop/m3d1r/assets/152776722/191c827f-01f0-4b59-b362-e2fb441c1eaa)

- we will run that code in the javascript online 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/d8ab3155-189a-4261-a934-aed4d37f53d0)

=> flag: picoCTF{p@g3_turn3r_6bbf8953}

## WebDecode

![image](https://github.com/j10nelop/m3d1r/assets/152776722/2adeb885-302e-416e-9709-1d798367adc9)

- open the terminal and i have to see the source code of this web site it's might be have some path for me to see

Recon 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/61c93ad9-9a2a-40b5-a2d2-3efaa1ec1561)

![image](https://github.com/j10nelop/m3d1r/assets/152776722/c0c98a8a-439e-453c-acad-dbfc81b0c43b)

- we could see the source code have and the hint told us to navigate that i think it could in the navigate container card

- we keep digging each of that link html till i found the about.html

![image](https://github.com/j10nelop/m3d1r/assets/152776722/2042c721-5969-4229-b71c-4a9b60f256fd)

- i think it might be base64 encode solve we decode it and we have

![image](https://github.com/j10nelop/m3d1r/assets/152776722/aa82d745-1b81-45fd-a8a3-6b043165850d)

=> flag: picoCTF{web_succ3ssfully_d3c0ded_1f832615}

## Unminify

![image](https://github.com/j10nelop/m3d1r/assets/152776722/f21acd83-3373-4588-817a-77a2d6a9a252)

Recon 

- ctrl + u  and see source code and to find this all we have to do is trying to grep the picoctf cause the source code kind of messy

- i using inspector to see each of part card in the html website after i search i found the flag

![image](https://github.com/j10nelop/m3d1r/assets/152776722/37d716be-f3f3-49b9-bef8-13085cdf56a1)

=> flag : picoCTF{pr3tty_c0d3_51d374f0}

## introtobrup 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/be2d881e-9064-47c5-87c7-11072ed110ba)

Recon 

- to solve this part we should using brupsuite to see the request
 
- after input the account from user we can see that otp is have from the method post


![image](https://github.com/j10nelop/m3d1r/assets/152776722/2998d786-4ef8-4d77-961a-c691b1dedae4)

hint:
Try mangling the request, maybe their server-side code doesn't handle malformed requests very well.

=> so we try to changing the request from get to post so we can see the flag 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/e14117f0-056a-4879-83e8-cbc714b17e6d)

=> flag: picoCTF{#0TP_Bypvss_SuCc3$S_6bffad21}

## Nosql injection 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/e33334d5-edc8-46eb-9a9e-f7a2673fdf5e)

Recon

- in this web we know this is the nosql injection exploit but how we can solve this first we need to download the script app from this web

- first i don't just locate the src code is from the login path so i need to find it and it's name route.ts file

![image](https://github.com/j10nelop/m3d1r/assets/152776722/7ab95975-b3d4-463c-9648-001d54bc02e0)

- i search the payload from the link:

https://book.hacktricks.xyz/pentesting-web/nosql-injection

- so i we know the code mention with the payload is the way to bypass that we using json strings

![image](https://github.com/j10nelop/m3d1r/assets/152776722/4cb3dab7-fd76-4462-8bc2-195bad1f3c05)

- back to login we test the first payload with

{"$ne": null}

i put in each email and password 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/f14150ec-aa2a-4794-a1e9-dc4bba1e6ccd)

- we see when they handle the payload we can see the request process has been add the backslash

![image](https://github.com/j10nelop/m3d1r/assets/152776722/1d450973-ac24-4382-afec-88a84957a7de)

![image](https://github.com/j10nelop/m3d1r/assets/152776722/c78183b2-ed3d-46cf-b05d-a2ae0a523400)

- it's require "{" because if we not using the blackslash that bracket would become the value so we need the \ to make sure it part of json strings

![image](https://github.com/j10nelop/m3d1r/assets/152776722/cfca9195-179c-456a-9e32-6fe9eaf814c9)

=> token so we identify as the base64 decode

after decode we have

=> flag: picoCTF{jBhD2y7XoNzPv_1YxS9Ew5qL0uI6pasql_injection_af67328d}

## trickster

![image](https://github.com/j10nelop/m3d1r/assets/152776722/aa179dbc-5011-4501-bbd7-bc1f664191da)

- we have the web upload the point of this that we need to upload the web shell to find the flag

Recon

- frist create an web shell we have

![image](https://github.com/j10nelop/m3d1r/assets/152776722/54bf0e49-59b9-4d05-ba5e-38b18110f1f8)

``` <?php system($_GET['cmd']);?> ``` 

to handle the command and managing directory on web server 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/bed1e8e0-768a-4d84-84f0-019c4b31dbf9)

- we get missing .png on the file so we config that and test again

![image](https://github.com/j10nelop/m3d1r/assets/152776722/21a8992c-cf38-439e-82d1-c35e72dcb69e)

- it seem we have some problem in hex image of my file so i need to search for that and i found the problem

- after i scan my web usin brupsuite pro i found the robots.txt and have an instructions.txt

![image](https://github.com/j10nelop/m3d1r/assets/152776722/49ea844e-e542-4304-ae4a-88c7ad4969c5)

- i found the problem in the magic bytes dosen't valid so i search to bypass and config my file

 ![image](https://github.com/j10nelop/m3d1r/assets/152776722/54b289d4-9c6a-424c-a473-c97fe2fdc91a)

- so i put on the start of my code for next valid image png

![image](https://github.com/j10nelop/m3d1r/assets/152776722/99d9d879-b577-4952-8c09-fe500e409a0e)

it's oke but 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/06b497d3-c18d-43ac-99e1-2939a6e9b179)

- this error because file format actualy is php but it's just modifile on web is wrong so i fix then it's oke


![image](https://github.com/j10nelop/m3d1r/assets/152776722/67d290d3-3f86-4b8a-b592-203648f06e6a)

there it's access on the image so i will control it's through url using ?cmd= 

- becase this web shell start with /var/www/html using ls -la list all the current dir we see ..

![image](https://github.com/j10nelop/m3d1r/assets/152776722/827b62d7-1aa3-497f-923d-bf021ae3027d)

=> we found the flag: picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_3f706222}
