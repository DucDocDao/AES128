# Đang cập nhật Vietnamese...
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
### * Example:
<img width="511" height="179" alt="image" src="https://github.com/user-attachments/assets/0d72cb01-2fae-4862-b976-863fe9ddae13" />

#### To calculate 04, we need: 02.d4 in the calculation.
#### To calculate 66, we need: 02.bf in the calculation.
#### To calculate 81, we need: 02.5d in the calculation.
#### To calculate e5, we need: 02.30 in the calculation.
#### Similar to 03 and 01.
### => Once we know the byte position to calculate, we just need to change the byte position of the state matrix to multiply by the byte of the fixed matrix (I know what I say will be difficult to understand, you can refer to the design to visualize better).
## 5. Key Expansion: 
### * 5.1: About Rcons: I will design each one separately and package it because we only need 10 Rcons.
### * 5.2: In my designs, I have to create 10 Key Expansions for each key after each round because the total pins of Quartus is only 475, if we design Key Expansion in just 1 design, it won't be enough.
<img width="574" height="319" alt="image" src="https://github.com/user-attachments/assets/ebf573be-8b2f-4ea8-a1cf-5d061d8f09e7" />

## 6. 
### * 6.1: Counter-4-bit: to count to 10, which is the last round of the algorithm: decides when the last result will be received.
### * 6.2: Start = 1: starts loading data and keys into the algorithm for encryption.
### * 6.3: Done = 1: end of algorithm (Counter counts to 10).
