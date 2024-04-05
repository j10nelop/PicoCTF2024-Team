## Forensic:

### Scan Surprise
* ssh -p 49849 ctf-player@atlas.picoctf.net
* 83dcefb7
* Sau khi vào được máy chủ của bên pico thì mình thấy ngay một hình ảnh mã qr, sau khi ls thì có một file là flag.png nên mình đoán ảnh QR ở đầu chính là file này

![Screenshot 2024-04-05 121331](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/3ebfad66-5996-4938-86c9-763e73d9c3fb)

* Quét QR và mình tìm được flag, flag được encode trong ảnh QR

![ảnh](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/57eed1b2-6287-4ef7-98cb-8202fae3e2c5)

`Flag: picoCTF{p33k_@_b00_3f7cf1ae}`

### Verify
* ssh -p 51194 ctf-player@rhea.picoctf.net
* 83dcefb7
* mình tải file challenge.zip đề bài cho thì có file checksum.txt là chứa một mã băm, một file decrypt.sh và một folder chứa các file có nội dung

![Screenshot 2024-04-05 125658](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/ac93a485-0699-4ff6-bf30-1cea1e2892cf)

* file decrypt.sh này chứa lệnh ``openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000 -salt -in "/home/ctf-player/drop-in/$file_name" -k picoCTF`` sử dụng để decrypt mã hóa aes với độ rộng bit là 256 mode CBC với một file truyền vào
* ssh vào máy chủ bên đó, mình đoán là checksum.txt sẽ chứa mã băm của một file nào đó trong folder file nên mình đã sử dụng lệnh ``sha256sum files/* | grep $(cat checksum.txt)`` để băm các file trong folder file và so sánh với checksum.txt

![Screenshot 2024-04-05 131324](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/57089a58-d54a-474c-b35d-28f9dc943e8c)

* sau khi tìm được file chứa nội dung giống checksum.txt thì mình sử dụng decypt.sh để decrypt file này thì mình được flag

`Flag: picoCTF{trust_but_verify_c6c8b911}`

### CanYouSee
* Sau khi giải nén tệp đề bài cho thì mình được một bức ảnh

![ukn_reality](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/9ef9debf-ae1f-4545-9f41-1fca434f41b4)

* Không có gì nên mình đã thử exiftool để xem metadata của file thì mình thấy có Attribution URL                 : cGljb0NURntNRTc0RDQ3QV9ISUREM05fZGVjYTA2ZmJ9Cg== một đoạn mã đã được mã hóa base64
* Mình decode và ra flag

![Screenshot 2024-04-05 133628](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/f1447ddc-490a-4bdc-904e-0870b8efd71a)

`Flag: picoCTF{ME74D47A_HIDD3N_deca06fb}`

### Secret of the Polyglot
* Mình mở file của đề bài cho thì là một file pdf có chứa nửa flag cuối

![Screenshot 2024-04-05 134112](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/b49dfbfc-96d6-4dd8-87f2-355146c4b600)

* Sau đó mình exiftool xem metadata và thấy được rằng định dạng của file là png nên mình đã đổi extension thành png và mở ra được nửa flag đầu

![Screenshot 2024-04-05 134416](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/f70f84a3-823a-4476-9e8c-c475aa14a0da)

![Screenshot 2024-04-05 134449](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/1bb216b1-2d7e-4141-9207-866496f3ab56)

`Flag: picoCTF{f1u3n71n_pn9_&_pdf_53b741d6}`

### Mob psycho
* giải nén file apk bằng 7zip và chúng ta được một folder mobpsycho, mình mở thử folder META-INF và res thì thấy có rất nhiều folder nhỏ bên trong nên mình đã nghĩ đến rằng flag sẽ nằm ở đâu đó trong folder này
* 
![Screenshot 2024-04-05 141845](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/757d8379-5ad0-4c28-89c1-3e1c6cf215e0)

`find -name "flag*"`

* mình dùng lệnh find để tìm tất cả các file hoặc folder có tên bắt đầu bằng flag và mình đã tìm thấy file flag.txt, sau khi mở file thì đây là một đoạn đã được mã hóa dưới dạng hex nên mình đã decode nó và ra được flag

![Screenshot 2024-04-05 141651](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/2ed48d92-1af7-4df5-b9e5-294b913ce92d)

`Flag: picoCTF{ax8mC0RU6ve_NX85l4ax8mCl_52a5e2de}`

### endianness-v2
* mình thử exiftool thì hiện warning Processing JPEG-like data after unknown 1-byte header nên mình đã thử mở file bằng hxd

![Screenshot 2024-04-05 142816](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/9dacd3ac-3a35-4667-bbfd-c241be179400)

* lúc đầu mình đọc rồi so sánh với định dạng file thì thấy có vẻ giống với hex header của jpeg nên mình đã thử sửa và mình chú ý rằng các byte này đã bị xáo trộn một cách có quy tắc, các byte đã bị đảo ngược theo cụm mỗi 4 byte nên mình đã viết code để đảo ngược lại chúng về đúng thứ tự

```
package reversehex;

import java.util.*;
import java.io.*;

public class ReverseHex {

    public static void main(String[] args) {
        String originHex = "E0 FF D8 FF 46 4A 10 00 01 00 46 49 01 00 00 01 00 00 01 00 43 00 DB FF 06 06 08 00 08 05 06 07 09 07 07 07 0C 0A 08 09 0B 0C 0D 14 12 19 0C 0B 1D 14 0F 13 1D 1E 1F 1A 20 1C 1C 1A 20 27 2E 24 1C 23 2C 22 29 37 28 1C 34 31 30 2C 27 1F 34 34 32 38 3D 39 34 33 2E 3C 00 DB FF 32 09 09 01 43 0C 0B 0C 09 18 0D 0D 18 21 1C 21 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 32 C0 FF 32 32 00 08 11 00 03 2C 01 96 02 00 22 01 11 03 01 11 00 C4 FF 01 01 00 00 1F 01 01 01 05 00 01 01 01 00 00 00 00 01 00 00 00 05 04 03 02 09 08 07 06 C4 FF 0B 0A 00 10 B5 00 03 03 01 02 05 03 04 02 00 04 04 05 01 7D 01 00 04 00 03 02 21 12 05 11 13 06 41 31 22 07 61 51 81 32 14 71 23 08 A1 91 15 C1 B1 42 24 F0 D1 52 82 72 62 33 17 16 0A 09 25 1A 19 18 29 28 27 26 36 35 34 2A 3A 39 38 37 46 45 44 43 4A 49 48 47 56 55 54 53 5A 59 58 57 66 65 64 63 6A 69 68 67 76 75 74 73 7A 79 78 77 86 85 84 83 8A 89 88 87 95 94 93 92 99 98 97 96 A4 A3 A2 9A A8 A7 A6 A5 B3 B2 AA A9 B7 B6 B5 B4 C2 BA B9 B8 C6 C5 C4 C3 CA C9 C8 C7 D5 D4 D3 D2 D9 D8 D7 D6 E3 E2 E1 DA E7 E6 E5 E4 F1 EA E9 E8 F5 F4 F3 F2 F9 F8 F7 F6 00 C4 FF FA 03 00 01 1F 01 01 01 01 01 01 01 01 00 00 00 01 01 00 00 00 05 04 03 02 09 08 07 06 C4 FF 0B 0A 00 11 B5 00 04 02 01 02 07 04 03 04 00 04 04 05 00 77 02 01 11 03 02 01 31 21 05 04 51 41 12 06 13 71 61 07 08 81 32 22 A1 91 42 14 23 09 C1 B1 15 F0 52 33 0A D1 72 62 E1 34 24 16 18 17 F1 25 27 26 1A 19 35 2A 29 28 39 38 37 36 45 44 43 3A 49 48 47 46 55 54 53 4A 59 58 57 56 65 64 63 5A 69 68 67 66 75 74 73 6A 79 78 77 76 84 83 82 7A 88 87 86 85 93 92 8A 89 97 96 95 94 A2 9A 99 98 A6 A5 A4 A3 AA A9 A8 A7 B5 B4 B3 B2 B9 B8 B7 B6 C4 C3 C2 BA C8 C7 C6 C5 D3 D2 CA C9 D7 D6 D5 D4 E2 DA D9 D8 E6 E5 E4 E3 EA E9 E8 E7 F5 F4 F3 F2 F9 F8 F7 F6 00 DA FF FA 00 01 03 0C 11 03 11 02 F7 00 3F 00 80 A2 28 FA 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 77 AA 28 0A A6 9B B6 DA A1 86 1A 14 04 64 68 69 58 26 DA A7 48 80 01 F7 E5 C6 19 C9 00 AD C7 FC E5 B3 A2 5C 64 DB F4 D6 AD AF EE 99 44 29 92 6D 8A 4E D3 2C 07 0E 15 37 07 56 09 5E 38 07 07 07 CF CB 14 C1 22 36 E9 10 81 BE 65 E5 F2 40 B7 A7 69 20 C7 5B 60 03 C0 79 A0 2C C9 39 B4 1E 96 7A 64 45 A7 01 32 C9 AE 43 B5 D1 20 DC 23 80 BB 05 21 79 A3 35 C1 70 BE CA 7C 84 CD BC E3 59 FC AD B3 CF 4A A7 8F BF 98 F1 07 7D 6B 4D DA A8 73 55 E6 BA E5 B5 F9 0A 13 DC B8 CC 31 7F 8E 53 EB 1F 0E A0 78 BD 8B C5 8A 9E 7D 82 B6 C4 1A BC 5F 44 09 77 36 7C DC 5C E6 6D A1 91 EF 2A 18 F4 48 49 39 C1 01 12 13 74 FC C1 F9 92 B0 52 D9 F6 52 AC 35 77 15 AF 40 A6 CA BA 73 AE E4 38 40 E7 47 8E 76 AE A8 16 1F 1E C7 FB 5D A4 89 B2 F4 AF 0B 42 6D 91 EF 29 91 0C 49 65 5E 38 03 C2 20 07 5B 70 43 1F 9C 67 E2 78 DF 50 71 FB C3 C2 84 7B DE 9A 71 52 D9 D1 27 47 B6 6B ED 58 F3 CB 7F A1 CA CF 04 19 88 89 75 80 1C 75 C6 4D 56 14 A4 D6 62 B8 2F D3 E0 D2 08 8A E5 6E 31 E1 91 A7 9D 91 45 04 49 DD 3B 57 03 BA 8D 39 88 17 9D DA 71 8D CB 74 A8 6B 8B 74 32 8C 2E EE 15 19 E2 CA 46 5B 5E C4 95 83 AF AC 31 30 C8 6C 06 50 FA D8 AB 9D 15 A5 2D BA 56 EB C8 C5 D5 A5 39 7B 5B 66 97 11 19 AF 16 40 A4 7B 4F 82 A4 DA 92 91 DB 23 AF BD 2A 32 91 EB 34 8A 24 9E DB 64 EF 9A B4 BA 0A 51 D8 7C 8B AC D1 C4 C0 CA CF 21 06 1D 01 C8 40 8E E7 D6 3B AC 68 36 97 69 16 5F A3 05 69 B7 FF F7 EA B4 A2 49 60 00 9F B4 F1 2A 43 46 FB 66 E3 ED CA 03 8C 71 77 3D C5 8F 4F 73 7A EA 53 3A 08 DC 93 9D 3E 84 B3 7F 91 10 F3 7C 55 65 56 66 72 27 4F 0C 0E E4 3E 15 D9 00 40 4E DF D9 AB A2 E2 36 6A 5A 0B EA CA E2 49 20 09 98 91 D4 81 04 54 71 64 D4 A6 4B 7C 2F E2 6D CA DA BC 6F 2F 9D 76 EC 83 D5 BC 4D 23 B2 60 41 70 82 F3 63 85 17 00 9A C2 11 2D B3 A2 D7 EE 36 FD 35 54 FB 47 0B 5D 76 49 70 54 77 82 62 D7 36 B2 90 AB E4 B9 50 6A 9E 71 70 90 46 F1 26 79 CB 6E AD C7 B3 96 14 14 77 89 2C ED FE F0 8A 07 96 32 43 7D CB 6D EF 03 28 BD 15 35 A2 8A 62 D4 54 74 30 0F D8 A5 8D 79 5B 94 10 C2 91 9B 79 73 EF 07 ED CD 1D B8 8E 36 F1 B6 54 F2 BC 25 9B 69 BA 4A DE CA DA E0 82 85 C6 B2 97 DB 24 08 64 C8 4F C5 90 19 4F 70 77 D9 00 38 F4 BC AE B1 A2 36 57 04 47 5C DA 58 30 04 79 6D 6A 93 35 11 B7 8C CB 57 C4 EE DC 09 C6 E3 22 F3 A0 B7 4E EF 19 3D 93 36 F1 E4 BD 5D 9B 2B 22 F0 36 B1 C8 DC BB B8 CC DC EC EE 54 4E 60 E5 40 5E 46 A0 C1 19 48 84 2A 7A 0D 6D 91 E6 FA 6A DC 70 34 2A 4B 51 96 5C 92 46 AB 48 0C 97 22 82 3C 01 52 0D AE C7 41 B7 65 9E 5B 0E 67 92 B7 C1 2E 35 52 0C 60 B3 10 FB 24 07 F0 4A 02 68 0E C6 8B 9C 2B B6 16 D7 36 EA A6 C1 B2 D7 70 4D 12 8D 6D 5B 20 9E 04 41 24 38 B7 85 5C 19 C7 86 51 E0 3A 3D CF 75 9A C6 87 41 D0 C2 CB 8F A4 25 75 C2 DA 1F 6F 75 5E 8D A8 2C 48 8D 46 72 22 91 1F 93 BB 81 14 47 07 C0 C1 E2 CB 62 45 43 ED 0F 7B A8 13 59 A6 95 65 88 DE 26 96 B4 A1 6A BC E5 29 05 9C DB CA 0E 0E C8 6C 00 77 EB 3E 36 C6 13 18 5E 33 0C 0B 1C 9F 3E C1 EF 58 D2 B7 AB 82 68 BA C5 EC 6E A4 FD ED CA 95 9D 73 2E DB 40 EF 18 C3 80 15 0D 1D FE D3 2E DE 1C C5 E4 DB E1 89 5B D3 8A C8 6B B7 42 49 22 34 DC DE C7 98 AA 9C DE D9 E0 75 F3 91 12 EF 6B E2 9B 47 5B 59 1E AF ED 59 6E 2D C8 3B 2D 75 8A 23 88 55 96 09 0C 79 06 12 01 8E 83 C3 9A 0D A0 F4 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 4D FB B5 E5 E9 16 6F 4A 5B 59 D8 33 EF D3 04 5C 2C BA 76 63 B7 77 29 B1 B9 15 DC C0 80 3B 6E 38 40 D1 D4 D5 E0 9F 26 1C 9C 45 53 DD 8D 25 6B 4D 09 0C 8D E9 AB B2 DB 1D 87 B5 B5 A1 E6 5B 61 7B EE 78 6C DD 1D 15 79 AE 29 B5 81 C7 92 6C AD ED AC 18 3E 5D B6 52 DF 2F 9E C1 30 9E 36 D2 C5 52 C3 58 18 8F 70 62 38 36 FD 5D 31 8A A7 9F 01 14 9E A5 59 0D C4 5A 4C 6D B7 62 15 AC 13 C8 90 B7 CA C5 DC 19 71 E4 24 A9 D4 A3 0D 8C 83 8F 05 D6 33 7C 48 E6 2E E4 E4 15 94 3D A4 95 58 EA D6 C6 67 3F A5 59 A4 4D 56 C1 AE 9F EE AF 9D 1E AF 3A C5 01 14 7D D0 EA 0F 9F FE FE 8E F8 58 D2 DE D2 31 F9 D2 CC 6E 44 4A DE AC 6E C3 92 70 9B 01 D9 39 82 5B 78 74 69 70 0E E9 DC 07 5F 49 13 C4 9A B7 B7 76 F6 39 E6 9E B9 B2 7E E6 12 02 56 1B 06 E6 0B B4 7C 00 4F 0E 10 EC 9A 93 71 20 0E A0 E8 FB EF 32 78 18 D3 48 03 E8 5B 32 DB D0 45 1A 17 69 79 4C 49 0E B9 11 12 1E 51 FC C3 E0 2C FE 48 FF 4A 07 E3 77 D7 C3 00 2D 8C 47 5A 9A 04 48 12 72 F6 99 D7 AD BB 70 CC E3 6F 84 23 E3 09 99 8F 15 BF 63 3C 1C 40 D1 D2 EA A1 A1 BE 4D BA 78 12 E5 28 DE 5A E1 2D ED 81 3D A7 FD 0B 49 8E 56 A9 A9 B1 92 58 63 90 08 0E AA F5 A1 77 AB 81 46 9A 6D BA D7 68 B7 F6 D6 C4 5C 7A E9 10 96 FD 11 D6 96 DC DF 4F 0E B1 4A 78 11 91 54 15 93 3C 6E 24 9D 1D CF C9 6B C9 01 14 E2 A1 2E DA 8E E4 79 5B 26 2F EC DF 88 A7 7F 8F 09 77 DD AE 31 B6 F2 26 BF 8D CB F2 9E F3 6C BB AA A7 1A 9C B9 50 2F F8 96 D7 14 F1 89 AD DA 73 09 8E A6 89 06 ED 67 4B 4E 59 79 7B FD 5B 1E 01 76 F9 9E 9F E6 AE 39 38 34 E5 00 8A DE 0D 00 FF EB 6B BE FD D2 0C 6F E1 22 A8 ED 6A 8C 48 4C DA CE 6F 31 1B 9D 63 FE E8 0E EA A0 C7 9F E7 84 7F 34 43 5C 00 BD A8 C5 F1 9C AE 9B D5 99 BD 3B A2 4F DB 05 61 8C 91 ED 26 49 70 AC 92 77 9B 99 25 28 BA 3B 62 6F 18 06 03 5E CD 6B 34 BE 26 2C E5 3C E1 FB 5B 86 F1 6A 69 19 43 10 45 0C 32 E6 DD 13 BA 8D EE FC 17 56 D4 F8 CA 9A 22 DD 5A 0D 82 5B 4B 22 6C B6 A2 AE 99 8F F9 98 79 3B D9 60 29 C8 F2 C5 18 AB B3 82 E5 77 05 0E 3E 33 07 50 74 E6 6E F8 A4 2F D3 53 C7 A0 1D 78 27 B7 CD FC 82 3C 73 4D 3C 1F 99 1D 73 93 71 6D 74 4E 8E D3 83 84 00 FF 21 1E F0 E4 49 B6 4C A0 89 D8 87 35 AF C3 CE D3 7C B8 79 3A E5 89 72 27 E3 76 67 20 07 AC 6B 32 0E 6F 32 80 A2 8C 49 B5 2E 13 36 D6 D6 D1 90 2A 41 30 62 4E DD 4E 25 08 BE 32 0C B8 1C 9C 91 DB B9 85 97 35 D6 3D 5D 8A 27 21 18 2B DE 44 7D 58 83 8E 49 40 DA 10 CF 36 15 93 D1 CE 58 F0 90 30 E6 0C 7A B3 BC 07 50 F4 F5 6B A0 6D 21 A5 FD 5D 3A 17 76 A4 DD 86 A9 23 06 88 87 5B 8E 59 BA B9 05 B6 11 C1 A3 30 82 AB 70 54 13 3C 39 D5 0C E1 BF F6 0C AE AD B4 92 16 F7 19 CE 4B 9E E6 EF 22 DA D6 2E C9 5D BA 31 C6 0A 9C 23 48 E5 73 46 2E 2B 01 14 E5 5D 8B E0 43 C2 ED E5 F0 E4 D7 68 C9 8B DF 66 78 53 CD 4D 8E 47 98 35 96 85 84 DC CE 31 EB 39 44 26 5D 81 E3 C1 BD B3 77 7C 99 36 DB FB 9C 4B 1C 77 E5 45 33 5D 2F 07 D0 B7 A2 5C AD F9 BF 8B 38 80 5B DC DC 06 E9 DA 93 40 DC 71 94 9A 4B 9B 12 EA FB 11 61 C7 3E 22 ED 44 AA CE 37 76 36 FE F4 4A 70 4C E8 C1 2D F6 22 78 5A 79 D2 46 5E 78 EA CA B4 00 FF D1 89 B9 C8 E5 8D 57 44 61 5F 1B 69 17 0F F3 93 6B C0 C1 AD F5 00 8A EE AE 0D DF B4 E2 D6 6C BA EB 66 F6 1F 4F 9F 48 37 ED CC 97 B6 4F 34 3B D3 72 B3 41 1E 45 48 A2 FB 81 5C 4F F2 04 C3 FB 7E F1 F8 D8 30 B7 6D 2D 1D 7A EC 26 6D A6 46 F2 C2 4E 32 F7 37 4F 5B C1 6D A1 6C 20 2D E7 74 4D AE E3 9E 07 50 D4 BC 01 FE E9 CC 45 D4 B4 33 C9 A6 A9 BD F0 A5 DF 8B D6 79 CB C4 DB 7B BF CB 19 F3 0A 24 5E EE 8C A1 55 3A 6E 2D 5A BD E1 7B 4B C7 16 D5 56 09 5B C4 C5 2D AD 42 B2 4C 4C CE C8 A3 93 44 B9 0D 58 4B DC 55 39 B8 2B 72 36 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 28 0A 80 A2 FF 3F 80 A2 D9";
        String[] hexArray = originHex.split(" ");
        String[] reversedHexArray = new String[hexArray.length];
        
        for (int i = 0; i < hexArray.length; i += 4) {
            if (i + 3 < hexArray.length) {
                reversedHexArray[i] = hexArray[i + 3];
                reversedHexArray[i + 1] = hexArray[i + 2];
                reversedHexArray[i + 2] = hexArray[i + 1];
                reversedHexArray[i + 3] = hexArray[i];
            }
        }
        StringBuilder reversedHex = new StringBuilder();
        for (String hex : reversedHexArray) {
            if (hex != null) {
                reversedHex.append(hex).append(" ");
            }
        }
        String filePath = "reversed_hex.txt";
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
            writer.write(reversedHex.toString().trim());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
* sau khi đảo code xong mình đã đổi lại hex trên hxd, đổi extension thành jpeg và mở ra flag

![Screenshot 2024-04-05 144350](https://github.com/LDV-SpaceK/picoCTF2024/assets/151914246/affd1049-9e6c-4c79-b75b-1c69a0b9c8ff)

`Flag: picoCTF{cert!f1Ed_iNd!4n_s0rrY_3nDian_188d7b8c}`


