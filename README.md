## picoCTF_questions
This repository contains writeup for helping in solving picoCTF questions by Richa Ganesh Shanbhag  
## 1)Flags
## Description
What do the flags mean?  
## Data provided
<img width="821" alt="flag" src="https://github.com/richashanbhag/picoCTF_questions/assets/149705539/9854f006-8b5c-488d-9d37-1207f36e8faa">  

## Hints
The flag is in the format PICOCTF{}  
## Approach
With the help of the hint given, the first 7 flags represent PICOCTF. Then, the rest of the flags can be decoded using the naval flag code. 
![image](https://github.com/richashanbhag/picoCTF_questions/assets/149705539/f4e25498-012d-475f-8d8b-f7871850fa90)

## Flag
```
PICOCTF{F1AG5AND5TUFF}
```
## 2)miniRSA
## Description
Let's decrypt this: ciphertext? Something seems a bit small.
## Data provided

N: 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e: 3

ciphertext (c): 2205316413931134031074603746928247799030155221252519872649649212867614751848436763801274360463406171277838056821437115883619169702963504606017565783537203207707757768473109845162808575425972525116337319108047893250549462147185741761825125 
## Hints
1)[RSA Tutorial](https://en.wikipedia.org/wiki/RSA_(cryptosystem))  
2)How could having too small an e affect the security of this 2048 bit key?  
3)Make sure you don't lose precision, the numbers are pretty big (besides the e value)  
## 3)transposition Trial
## Description
Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message.  
Download the corrupted message here.
## Data provided
heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V6E5926A}4 
## Hints
Split the message up into blocks of 3 and see how the first block is scrambled
## Approach
As it is given in the description, that the first word is 3 letters long. If we change the position of letters in the first block of word 'heT', we can decode the transposition pattern. If we change the order of letters from'123' to '312', then 'heT' will become 'The'. Thus, if we follow the pattern '312', then we can decode the given text   
We can write a python code to decode the rest of the given text. We need to create two lists, one list called 'c' which contains the cipher text and an other list 'f' which is empty. Then, with the help of a for loop, which iterates over the c list with a step of 3. It starts at index 0 and goes up to the length of c. We need to take block of 3 characters and then, change their positions from'123' to '312' and append this to the empty list 'f'. Then, we can join the elements in the list 'f' by using ''.join(list).
## Commands 
```
c = list('heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V6E5926A}4')

f = []

for i in range(0, len (c), 3):
    f.append(c[i+2])
    f.append(c[i])
    f.append(c[i+1])

print(''.join(f))
```
# Flag
```
picoCTF{7R4N5P051N6_15_3XP3N51V3_56E6924A}
```
## 4)Substitution 1
## Description
A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again.  
Download the message here.
## Data provided
SYTe (eakdy tkd sjbyndr yar thjm) jdr j yobr kt skxbnyrd ersndzyo skxbryzyzkc. Skcyreyjcye jdr bdrercyrq gzya j ery kt sajhhrcmre gazsa yrey yarzd sdrjyzwzyo, yrsaczsjh (jcq mkkmhzcm) evzhhe, jcq bdklhrx-ekhwzcm jlzhzyo. Sajhhrcmre nenjhho skwrd j cnxlrd kt sjyrmkdzre, jcq garc ekhwrq, rjsa ozrhqe j eydzcm (sjhhrq j thjm) gazsa ze enlxzyyrq yk jc kchzcr eskdzcm erdwzsr. SYTe jdr j mdrjy gjo yk hrjdc j gzqr jddjo kt skxbnyrd ersndzyo evzhhe zc j ejtr, hrmjh rcwzdkcxrcy, jcq jdr akeyrq jcq bhjorq lo xjco ersndzyo mdknbe jdkncq yar gkdhq tkd tnc jcq bdjsyzsr. Tkd yaze bdklhrx, yar thjm ze: bzskSYT{TD3UN3CSO_4774SV5_4D3_S001_7JJ384LS}
## Hints
