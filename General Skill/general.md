# General Skills 

## Super SSH


![image](https://github.com/j10nelop/m3d1r/assets/152776722/0832da30-d492-49af-bc71-65aa096f6637)

- open web shell terminal

+ connect to ssh using account ctf-player and password 83dcefb7

![image](https://github.com/j10nelop/m3d1r/assets/152776722/e7b0d5ae-a0fa-4527-8c09-3c00a82c5197)

=> flag: picoCTF{s3cur3_c0nn3ct10n_8969f7d3}


## Commitment Issues

![image](https://github.com/j10nelop/m3d1r/assets/152776722/11c759ae-98b2-4243-9d5a-faa8b4a6ba37)

- open the terminal install the challenge zip file we using "wget [url]" to install => then we unzip the file we get alot of git file

=> may be this skill gonna be using git to find all the respository history 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/b1a4c002-d343-4ca3-8e7f-49134d098ad6)

=> first thing we need to checking list all of that commit by using "git log" 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/82d2dfe8-905b-4a4f-88e6-8a4fd83504e5)

we can see the commit id for creating the respository to 

## Time Machine

![image](https://github.com/j10nelop/m3d1r/assets/152776722/d6ada9a4-c5f9-400e-8fdc-0c854b0a01b2)

- open terminal install the challenge zip and unzip the file 

+  using git log to know the history of commit

![image](https://github.com/j10nelop/m3d1r/assets/152776722/b6c6bf47-2d2b-40e9-8f35-831b7339fbc4)

=> flag: picoCTF{t1m3m@ch1n3_d3161c0f}

 
## Blame Game

![image](https://github.com/j10nelop/m3d1r/assets/152776722/515f2163-0234-4bba-bbf8-d3f6428d3d3b)

+ open terminal and download unzip challenge.zip

+ git log --follow <file> : using to trace the history commit respository 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/e32713c3-37a4-4474-bbae-5885e46f8745)

=> flag: picoCTF{@sk_th3_1nt3rn_b64c4705}

## Collaborative Development

![image](https://github.com/j10nelop/m3d1r/assets/152776722/40ac752f-f1fb-4279-b9e0-bbd063eb858c)

- open terminal download and unzip challenge.zip

+ in this challenge we need to show all the branches using git branch -a 


![image](https://github.com/j10nelop/m3d1r/assets/152776722/f01f6f32-e561-4770-9788-3f4c4e2dfed3)

=> then we have 3 part of that branch so we need to switch in to each of that part using git switch <part>

then see the changing of flag.py 

cat each for flag 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/4238c67d-870c-45dc-bef9-8da1acfc9a97)

=> flag: picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_e4b79efb}


## binhexa

![image](https://github.com/j10nelop/m3d1r/assets/152776722/edb55c88-c524-4c9c-8c08-471ce706945f)

Recon 

- we can see that we have operator math with 2 binary to solve this with limited time

![image](https://github.com/j10nelop/m3d1r/assets/152776722/9482328c-981a-4b62-b541-5c6f1ce9bcc3)

- i create a script to list all the operator and calculate the bin to solve

![image](https://github.com/j10nelop/m3d1r/assets/152776722/33a59cb4-702d-4301-bca3-d84e1b5a9fad)

 ```
 #/usr/bin/env python3

bin1=int(input(), 2);
bin2=int(input(), 2);

result_and = bin1 & bin2
result_or = bin1 | bin2
result_xor = bin1 ^ bin2

result_add = bin1 + bin2

result_sub = bin1 - bin2

result_mul = bin1 * bin2

result_left_shift = bin1 << 1
result_right_shift = bin1 >> 1

result_left2 = bin2 << 1
result_right2 = bin2 >> 1

print("bitwise and:  ", bin(result_and))
print("bitwise or:  ", bin(result_or))
print("bitwise xor`:  ", bin(result_xor))
print("bitwise add:  ", bin(result_add))
print("bitwise sub:  ", bin(result_sub))
print("bitwise mul:  ", bin(result_mul))
print("bitwise left:  ", bin(result_left_shift))
print("bitwise right:  ", bin(result_right_shift))
print("bitwise left2:  ", bin(result_left2))
print("bitwise right2:  ", bin(result_right2))
  

```

=> all we have to is run and copy paste the result 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/08b4c1db-d286-4d0f-b694-2e3eb895e220)

=> flag: picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_675602ae}


### Binary Search
* sau khi mở file guessing_game.sh thì file code này tạo ra một số random từ 1 đến 1000 nếu người dùng nhập vào một số bằng với số code đã tạo ra thì ra flag, mỗi một lần nhập số vào, nếu số của người dùng nhỏ hơn số tạo ra thì in ra màn hình Higher, ngược lại là Lower

![Screenshot 2024-04-05 150425](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/7a6731b8-68e6-4474-8961-035ff7322653)

* Mình đã sử dụng nguyên lí của thuật toán binary search là lấy giá trị phần tử ở giữa của mảng rồi so sánh với target, nếu nhỏ hơn thì tiếp tục lấy giá trị giữa của mảng phía trước, lớn hơn thì ngược lại

![Screenshot 2024-04-05 150058](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/465cb603-9a8b-4d8a-8271-e786e4299dd2)

`Flag: picoCTF{g00d_gu355_ee8225d0}`

### endianness
* đọc file source thì chương trình này tạo ra một chuỗi string random với độ dài 5 kí tự và sử dụng hai hàm find_little_endian và find_big_endian để tìm big và little endian của string đó, sau khi người dùng nhập vào thì tiến hành compare với string được convert bởi 2 hàm trên nếu đúng thì cho ra flag
* Mình đã tận dụng hai hàm đó để biến đổi chuỗi input bất kì thành big và little endian của nó
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>
#include <ctype.h>
#include <time.h>

char *find_little_endian(const char *word)
{
    size_t word_len = strlen(word);
    char *little_endian = (char *)malloc((2 * word_len + 1) * sizeof(char));
	size_t i;
    for (i = word_len; i-- > 0;)
    {
        snprintf(&little_endian[(word_len - 1 - i) * 2], 3, "%02X", (unsigned char)word[i]);
    }

    little_endian[2 * word_len] = '\0';
    return little_endian;
}

char *find_big_endian(const char *word)
{
    size_t length = strlen(word);
    char *big_endian = (char *)malloc((2 * length + 1) * sizeof(char));
	size_t i;
    for (i = 0; i < length; i++)
    {
        snprintf(&big_endian[i * 2], 3, "%02X", (unsigned char)word[i]);
    }

    big_endian[2 * length] = '\0';
    return big_endian;
}

int main()
{
    char challenge_word[10];
    scanf("%s",&challenge_word);
    printf("Little: %s\n",find_little_endian(challenge_word));
	printf("Big: %s",find_big_endian(challenge_word));
    return 0;
}
```

![Screenshot 2024-04-05 153229](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/69069a56-2e3c-401e-aebb-1cb0ffd7cc73)

`Flag: picoCTF{3ndi4n_sw4p_su33ess_817b7cfe}`

### dont-you-love-banners
* nc tethys.picoctf.net 56745 Mình thấy có một mật khẩu là My_Passw@rd_@1234
* nc tethys.picoctf.net 60233 trả lời các câu hỏi xong mình đã vào được server

![Screenshot 2024-04-05 153816](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/84d42d82-1c18-403f-8725-c01a036b4061)

* nội dung file text keep digging, nên mình tiếp tục cd về các directory trước và đề bài bảo mình phải tìm flag trong root nên mình đã vao root và tìm thấy file flag.txt nhưng mà không thể mở được do không có quyền nên mình đã thử chạy bằng sudo nhưng không được
* mình nghĩ đến cách truy cập vào user root để có full quyền nên mình đã thử `su -` thử password root thì không được

![Screenshot 2024-04-05 154142](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/89a935ab-a17a-4afd-bd17-c638ae37cd0e)

* mình mở file shadow để xem mật khẩu thì mật khẩu của root đã bị mã hóa

`$6$6QFbdp2H$R0BGBJtG0DlGFx9H0AjuQNOhlcssBxApM.CjDEiNzfYkVeJRNy2d98SDURNebD5/l4Hu2yyVk.ePLNEg/56DV0`

* `$6$` thì chúng ta nhận ra đây là mã băm sha512
* mình sử dụng hashcat để decrypt hàm băm này, viết dãy băm này vào file

`hashcat -m 1800 hashfile rockyou.txt`

* -m ở đây là mode 1800 là sha512, dictionary ở đây là rockyou.txt
* sau khi sử dụng hashcat thì mình được mật khẩu là iloveyou

![Screenshot 2024-04-05 163211](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/38313713-c7f1-429a-bbb6-3c16558bdc39)

* nhập mật khẩu vào root và mở file flag.txt mình được flag

![Screenshot 2024-04-05 155347](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/55b21628-4752-47d1-b3ba-bba95a134285)

`Flag: picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_68ca8b23}`
