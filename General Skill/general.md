## General Skill:

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
