# Semcms latest version(v3.9) allow Arbitrary file upload when it runs on a windows server whose hard drive patition is NTFS.
## 1st, Need Administrator's authority. Login as administrator First
![image](001.png)
## 2nd,upload a jpg webshell(just zero KB)
Choose a jpg webshell, whose content is "<?php phpinfo();?>"

![image](002.png)
![image](003.png)

Then click "Submit" in the page, see the HTTP request in Burpsuite.

![image](004.png)

Change the “wname” param to “111.jpg.php:”, as the follow picture shows.

![image](005.png)

And the response will tell you the path & filename(../Images/projoucts/111.jpg.php:.jpg) you just uploaded.

![image](006.png)

But, because of NTFS features, in fact, the system will create a file named **111.jpg.php** of 0KB rather than "111.jpg.php:.jpg".

![image](007.png)
 
## 3rd,Rewrite content to the zero-KB webshell
Send the upload HTTP request(we just mentioned above) to Burpsuite repeater.
Change it as follow.

![image](008.png)

And click “Forward” in Burpsuite, the response says we have created file 111.jpg<<<<

![image](009.png)

BUT, the truth is, from explorer's view, it is the 111.jpg.php has been rewrited! That's because the features of Windows.

![image](010.png)

Visit http://localhost/Images/prdoucts/111.jpg.php, and the php code executed.

![image](011.png)
