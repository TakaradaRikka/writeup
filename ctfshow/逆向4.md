## DIE
判断文件类型。

![image](https://github.com/TakaradaRikka/writeup/assets/44569515/9a1eb37b-9d69-4193-a81c-43026a36a8a1)
## IDA
尝试执行程序。

![image](https://github.com/TakaradaRikka/writeup/assets/44569515/89c28a43-294d-4b06-81de-90c8e3058b0f)

根据字符串交叉引用确定程序入口。

![image](https://github.com/TakaradaRikka/writeup/assets/44569515/3445d189-676b-4a2c-b0ba-dc9ae5597ae4)

* **主函数**

![image](https://github.com/TakaradaRikka/writeup/assets/44569515/63fc474e-a703-4dcb-ad55-df210062bb72)

调用了函数`sub_1400010E0`，传递参数为读取的输入`v0`。

* **函数sub_1400010E0**

![image](https://github.com/TakaradaRikka/writeup/assets/44569515/24ec5bc2-49f2-4279-927c-c23bc6186f84)

调用了两个函数，一个sub_1400011E0用于处理字符，一个sub_140001220用于程序进一步执行。

* **函数sub_1400011E0**

![image](https://github.com/TakaradaRikka/writeup/assets/44569515/4a34ee5c-cf95-4fa0-94ff-24a7e40406d7)


接收了从字符串尾部开始的逐个字符，与7异或（函数传参的时候）后将每个字符的地址保存起来。相当于对字符串进行了反转处理。

* **函数sub_140001220**

![image](https://github.com/TakaradaRikka/writeup/assets/44569515/59755578-89c1-407a-9971-034965d38078)

检查字符串是否和预设的一致。

## Python
```python
varbox2 = '/..v4p$$!>Y59-'
str1 = ''
for i in range(len(varbox2)):
    str1 += chr(ord(varbox2[len(varbox2)-1-i]) ^ 7)
# str1 = '*>2^9&##w3q))('

varbox = ')(*&^%489$!057@#><:2163qwe'
str2 = []
for i in str1:
    str2.append(varbox.find(i))
# str2 = [2, 16, 19, 4, 8, 3, 15, 15, 24, 22, 23, 0, 0, 1]

flag = 0
for i in range(len(str2)):
    flag = 26 * flag + str2[len(str2) - 1 - i]
print(flag)
```
