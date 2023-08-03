# Semcms latest version(v3.9) allow Arbitrary file upload when it runs on a windows server whose hard drive patition is NTFS.
## 1. We should log in to the Web Administrator Console.
![image](001.png)
## 2. Attempt to upload a webshell in PHP format.

###Choose a jpg webshell, whose content is "&lt?php phpinfo();?&gt"

![image](002.png)
![image](003.png)

### Afterward, click the "Submit" button, and then interupt and observe the HTTP request in Burp Suite.

![image](004.png)

### Manually change the “wname” param to “111.jpg.php:” in Burp Suite(see picture below).

![image](005.png)

## And the response will show the path & filename(../Images/projoucts/111.jpg.php:.jpg) you just uploaded.

![image](006.png)

## However, due to the characteristics of NTFS, the actual file will appear as a 0kb-sized "111.jpg.php," rather than the "111.jpg.php:.jpg" shown in response.

![image](007.png)
 
## 3. (Key point) Rewrite content to the zero-KB webshell

### Place the HTTP data packet from the recent "Submit" click into Burp's Repeater, preparing to make modifications before resending it once again.

### Manually modify it as follow.

![image](008.png)

### And then click “Forward” in Burpsuite, the response shows we have created file 111.jpg<<<< successfully.

![image](009.png)

### However, upon checking from the file explorer, there is no file named "111.jpg<<<<". Instead, the previously created "111.jpg.php" file has been overwritten and now contains new content.

![image](010.png)

### By accessing the webshell file from the URL http://localhost/Images/prdoucts/111.jpg.php, the malicious code is executed.

![image](011.png)
