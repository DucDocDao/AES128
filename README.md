# I hope you guys all know about AES128, so I will focus more on the design and idea!
## 1. AddRoundKey: we just only have to XOR the data and the corresponding encryption key, it's very simple so I think everyone can do it easily!

## 2. SubBytes:
### * Creating S_box: * 
#### -> You have to creat a .mif file which already have all sbox values, you can easily find it on Internet because I don't remember where I found it too =)), or you can create a .mif file from Notepad and add all the values but I think this way is just a waste of time!
<img width="640" height="320" alt="image" src="https://github.com/user-attachments/assets/430405a3-498c-469f-9d62-2097796893e6" />

#### -> After that, create a 1-port ROM of 8 bits x 256 words from Megawizard Plug-in Manager and access it from the sbox.mif file you just created, remember to package the design.
## 3. ShiftRows: Just concatenate the bytes of the input corresponding to the bytes of the output to be rotated, it's still very easy!
## 4. MixColumn: 
### * 4.1: Instead of shifting left 1 bit in the multiplication by 02, we can use an 8-bit full adder, then the sum will be equal to that value plus itself and we only take 8 bits in the sum.  You can try some examples to prove it! 
### * 4.2: Instead of creating an additional .mif file to save the values ​​of the fixed matrix (this will just waste hardware resources), we see that in the rows of the fixed matrix, the value 02 always appears once, the value 03 once and the value 01 twice, the rows only differ in the position of the values.


