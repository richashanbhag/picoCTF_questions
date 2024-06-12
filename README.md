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
## Approach
For an encrypted plain text m, the encryption function is c=(m^e)%n. Since e(e=3) is small, modulus function can be ignored.  In cases where the plaintext m is small enough, m^3 will be less than 𝑛 rendering the modulo operation unnecessary. Therefore, to retrieve m, it suffices to find the exact cube root of 𝑐.
After finding the cube root of c, Then we can convert resulting m to hexadecimal so later we  could decode it into plain text using a hex decoder. We get the output from the code as  7069636f4354467b6e3333645f615f6c41726733725f655f36303663653030347  which we can give it to a hex decoder to get the required flag as output
## Commands 
```
def find_cubic_root(n):
    ll = 1
    ul = n
    while ul - ll > 1:
        mid = (ll + ul) // 2
        if mid**3 > n:
            ul = mid
        else:
            ll = mid
  if ll ** 3 == n:
        return ll
    elif ul ** 3 == n:
        return ul
    else:
        return 0
c= 2205316413931134031074603746928247799030155221252519872649649212867614751848436763801274360463406171277838056821437115883619169702963504606017565783537203207707757768473109845162808575425972525116337319108047893250549462147185741761825125
m = find_cubic_root(c)
h = hex(m)
print(h)
```
## Flag 
```
picoCTF{n33d_a_lArg3r_e_606ce004}
```
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
1)Try a frequency attack
2)Do the punctuation and the individual words help you make any substitutions?
## Approach
As the flag is always in the format picoCTF{}, which is at the end of the given text. SYT seems to be representing CTF and bzsk represents pico. Even, j is the letter that is being used individually, which means it represents the letter a. Similarly, other letters are converted as:
abcdefghijklmnopqrstuvwxyz to  hpnrsjwlqaobguyxdecfqkvmti
## Flag
```
picoCTF{FR3QU3NCY_4774CK5_4R3_C001_7AA384BC}
```
After decoding, we get CTFs (short for capture the flag) are a type of computer security competition. Contestants are presented with a set of challenges which test their creativity, technical (and googling) skills, and problem-solving ability. Challenges usually cover a number of categories, and when solved, each yields a string (called a flag) which is submitted to an online scoring service. CTFs are a great way to learn a wide array of computer security skills in a safe, legal environment, and are hosted and played by many security groups around the world for fun and practice. For this problem, the flag is: picoCTF{FR3QU3NCY_4774CK5_4R3_C001_7AA384BC}
## 5)Dachshund Attack
## Description
What if d is too small? Connect with nc mercury.picoctf.net 31133.
## Data provided 
Welcome to my RSA challenge! e:  
75217029650811489846101405143137544056581523652455476981684720901005437272165384004084218456044190313015919073617974917163893252918652818687298047536991815977785833447157368854453466076262514218075612787230393946923324384901756897661132158637508973425901297264790497874387605894243932830183852602058904425555
n:  
116863202103666735032712019027037288095627793136813400654892977083248758502782551053118888945579953465899390427557663408179345400296492301154030856454328623177127021095339428020236627638784582103634627559176487167311385367950787967240899989669249527883543958401037310291588817502115187169847182311398257141621
c:  
6978640109945401095080063888724342171674419956931628378176717936442829583321957234096788363316508199839753631882002529786199716795103629230478798268549933300981518120792287228139584396009955441468661665539539401672028578028754359576171508620278794145566254227559072103063431966964494872689774635450807933508
## Hints
What do you think about my pet?  [dachshund.jpg](![dachshund](https://github.com/richashanbhag/picoCTF_questions/assets/149705539/ff7c0462-f536-47b1-aa91-daa250c72e58))
## Approach
With the help of powershell, we obtained the given data. The given data can be decrypted using Wiener attack. We can find out the flag with the help of the parametres using (Wiener attack)
## Commands
nc mercury.picoctf.net 30761
## Flag
picoCTF{proving_wiener_1146084}
