# Writeup Giải Summer CTF Training VSL 2025
- Lời đầu tiên e xin cảm ơn các a đã tạo ra những câu challenge để luyện tập hay. Sau đây e viết writeup các câu web e đã giải được.
# Upload file 1
- Description: If you found it inside my application, a gift 4 you
- Khi vào trang web hiển thị 1 from upload file như sau: 
- ![image](https://hackmd.io/_uploads/rkZGE6sNgg.png)
- Tới đây mình upload 1 hình ảnh chuẩn vào .
- Sau khi upload xong nó chuyển hướng đến phần thành công đã upload
- ![image](https://hackmd.io/_uploads/r1eUVpoVge.png)
- Nói như trên các chỗ này thường xảy ra lỗ hổng upload file mình tiến hành vào burpsuite để giải quyết thay đổi upload web shell
- ![image](https://hackmd.io/_uploads/SyijVTsNll.png)
- Tới đây mình đã bỏ qua được phần mở rộng và upload được shell php lên tới đây get content ra thì được như sau:
- ![image](https://hackmd.io/_uploads/r1pGHTiNel.png)
- Bypass thành công thì chỉnh sửa payload xem file flag nằm đầu ?
- Sau khi sửa đổi lẹnh ls để dò file flag thì đã thấy:
- ![image](https://hackmd.io/_uploads/H1A_SasEeg.png)
- ![image](https://hackmd.io/_uploads/SJAELTsEel.png)
- Tới đây chỉ lấy flag thôi: **VSL{upl04d3d_th3_m4lw4r3_i2nfnvu39fjd}**
# Beach Shop 0
- Description: Cái nóng của mùa hè đã khiến @ph4nt0m không chịu nổi. Để chống lại cái nóng này, @ph4nt0m đã quyết định đi biển. Trước khi ra đến biển, anh ấy đã ghé qua các shop online để mua kính bơi, và thật tình cờ điều này đã đưa anh ấy đến một chuỗi lỗ hổng nghiêm trọng trong trang web này :>
Good luck ae để tìm được nhiều bug như @ph4nt0m
Note: Flag nằm ở /flag.txt
- Khi truy cập vào trang web thấy 1 trang web đẹp mát mẻ với cái nóng mùa hè :+1: 
- ![image](https://hackmd.io/_uploads/Syc2LpoVge.png)
- Tới đây truy tìm manh mối ở hình ảnh thì phát hiện được đường dẫn : view-source:http://61.14.233.78:5000/images?file=surfboard.jpg
- Theo như kinh nghiệm hay làm thì tuyến đường file này dễ bị path travelsal với hint ở đề bài flag nằm /flag.txt
- Thì payload mình như sau: **../../../../../../flag.txt**
- Thu được Flag cuối cùng: **VSL{b34ch_sh0p4th_tr4v3rs4l_2idmwiq9@39!}**
# Watch Store
- Description: Mùa hè này, du lịch là điều hiển nhiên. @ph4n10m quyết định mua một đồng hồ để có thể flex các em gái khi đi du lịch. @ph4n10m ghé thăm một trang web nổi tiếng về đồng hồ. Sự tình cờ này lại đem đến một bất ngờ nữa.
@ph4n10m quyết định sẽ để bất ngờ này lại cho bạn khám phá
- Và câu này do team ra nên writeup chi tiết tại đây: https://hackmd.io/@AnhFuck/SkHov-gQge
# Beach Shop - Old Challenge
- Description: Nếu bạn thấy nó quen thuộc thì bạn thực sự là một hacker lâu năm của VSL đấy :3
Chúc may mắn nhé! (Tài khoản test: guest/guest)
- Chúng ta cùng truy cập website xem thử nào. 
- ![image](https://hackmd.io/_uploads/SJ9Xjl2Vel.png)
- Website khá đẹp mắt 
- Khi truy cập trang chủ, mình phát hiện có tính năng đăng nhập và đăng ký. Thử đăng ký với username admin → hệ thống báo tài khoản đã tồn tại. 
- ![image](https://hackmd.io/_uploads/Sk3ijln4gl.png)
- Nhận thấy tài khoản **admin** này đã tồn tại và tôi nhớ ra challenge này có mã nguồn của năm trước và tôi tìm được mã nguồn và phân tích và đi vào khai thác.
- ![image](https://hackmd.io/_uploads/S1cs3l2Nxg.png)
- Ở tuyến đường này ở index trang nó sẽ lưu username đăng nhập vào session 
- ![image](https://hackmd.io/_uploads/Byd1pe3Vxl.png)
- Ở tuyến đường này tức là khi chúng ta truy cập được admin thì chúng ta sẽ truy xuất flag sẽ hiển thị ở profile.
- Bây giờ chúng ta cùng tập trung ở tuyến đường khôi phục mật khẩu ở tk admin
- ![image](https://hackmd.io/_uploads/BJT0yZ2Egx.png)
- ![image](https://hackmd.io/_uploads/Bk5Jx-nVeg.png)
- Ở đây nó sẽ đọc tất cả các file trong thư mục username/questions
- Bây giờ mục tiêu khôi phục mật khẩu của admin thì mục tiêu phải đọc **home/admin/question** vậy thì chức năng đăng kí cho phép điều đó
- ![image](https://hackmd.io/_uploads/H1WrbWhVxx.png)
- Ở tuyến đường register này tức khi đăng kí nếu chưa từ khóa password thì nó không cho phép ngăn chặn truy cập password.txt
- mình sẽ ghi file này vào **/home/admin/questions** để từ đó khi reset mình trỏ file này và nội dung mình cũng đã biết
- vậy làm cách nào để có file /home/admin/questions/password.txt thì mục tiêu là chúng ta cần đăng kí 1 username **admin/questions** với question answer tự đăng kí
- Sau đó vào chức năng khôi phục password trên web với tên admin
- ![image](https://hackmd.io/_uploads/H1T-XWhEge.png)
- ![image](https://hackmd.io/_uploads/rJFSXW3Ngx.png)
- Khôi phục được **password.txt** của tk admin 
- ![image](https://hackmd.io/_uploads/Bk7u7Z3Vlg.png)
- Bây giờ chúng ta cùng đăng nhập với tài khoản admin
- ![image](https://hackmd.io/_uploads/SJTcm-nNle.png)
- Thu được Flag: **VSL{0ld_ch4ll3ng3r_p4th_tr4v3rs4l_g0_h0m3_29fmpwi0qfs}**

# Cruypto
## Beginner
- Description: @ph4n10m nhận được thông điệp kỳ lạ từ @d4kw1n mà anh ấy không hiểu. Các bạn có thể giúp anh ấy giải mã được không? 
- Thu được chuỗi hex dài: 56 6d 30 77 65 45 35 47 55 58 68 56 62 47 68 58 59 57 78 77 57 46 59 77 61 45 4e 56 52 6c 5a 79 56 6d 74 6b 54 6b 31 58 55 6e 70 57 56 33 68 33 56 47 78 4b 56 56 4a 73 57 6c 64 4e 61 6b 56 33 56 6b 52 47 53 31 49 79 54 6b 6c 55 62 46 5a 70 56 30 56 4b 53 46 64 73 5a 48 70 6c 52 30 35 58 55 6d 78 73 61 6c 4a 75 51 6e 42 57 62 47 51 77 54 6c 5a 5a 65 55 31 59 5a 47 6c 68 65 6b 49 7a 56 47 74 6f 63 31 59 79 53 6c 68 6c 52 30 5a 68 56 6e 70 47 63 6c 52 55 52 6e 64 6a 4d 55 70 56 59 6b 5a 47 56 6c 5a 45 51 54 55 3d
- Tôi sẽ chuyển hex sang mã ASCII
- ![image](https://hackmd.io/_uploads/SJp1IZhNxg.png)
- Tôi thu được mã base64 :+1: 
-Vm0weE5GUXhVbGhXYWxwWFYwaENVRlZyVmtkTk1XUnpWV3h3VGxKVVJsWldNakV3VkRGS1IyTklUbFZpV0VKSFdsZHplR05XUmxsalJuQnBWbGQwTlZZeU1YZGlhekIzVGtoc1YySlhlR0ZhVnpGclRURndjMUpVYkZGVlZEQTU=
- Sau khi decode nhiều lần cực khổ thu được:
- ![image](https://hackmd.io/_uploads/ryKHDWh4xx.png)
- Thu được Flag cuối : **VSL{53400e6416d46e613203bb6f877ebc80}**
