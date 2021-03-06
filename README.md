# MonoGen

Based off Pikaptcha by sriyegna, which is based off pikapy by skvvv, which is based off ptc2 Kitryn, which is based off ptcaccount by jepayne1138, etc.

## Description
MonoGen creates PTC accounts by creating a chrome session and automatically entering data in the required fields. If you choose to use the 2captcha service, the entire script can be run automatically, otherwise you will need to manually solve captchas.
MonoGen creates the PTC account and can verify emails.

## Installation
**For Windows**
Install the following clickable links: (if you cannot click them, all links are at the bottom.)

1. If you intend to manually solve captcha, you need [Google Chrome](https://www.google.com/chrome/) installed to default directory in C:\Program Files (x86)\

2. [Python 3.6](https://www.python.org/downloads/release/python-360/). Do this during setup. http://imgur.com/k421LiP

3. [Git](https://git-scm.com/download/win). Do this during setup. http://imgur.com/rhQi73O

4. If you intend to manually solve captcha, [Download Chromedriver](https://sites.google.com/a/chromium.org/chromedriver/downloads). Unzip the file and place it in %PYTHONDIRECTORY%\Scripts

5. Shift+Right Click your desktop and "Open command window here".

6. Type `pip3 install monogen` and hit enter

7. Refer to "How To Use" instructions below


**For OSX**

1. Open terminal and install chromedriver by typing `brew install chromedriver`

2. In terminal type `pip3 install monogen` without quotations and hit enter

3. Refer to "How To Use" instructions below


**For Debian based linux**

1. Open terminal and install chromedriver by typing `sudo apt-get install chromium-browser`

2. In terminal type `pip3 install monogen` without quotations and hit enter

3. Refer to "How To Use" instructions below

If an update is made to MonoGen, all you need to do to update is open CMD or terminal and type
    `pip install --upgrade monogen`

If you want to uninstall MonoGen, all you need to do to uninstall is open CMD or terminal and type
    `pip uninstall monogen`


## Using 2captcha
If you want to use the 2captcha service (if you cannot click the links, they are also at the bottom of the readme)

1. You need to download [PhantomJS](http://phantomjs.org/download.html)

2. You need to open the .zip file, open the phantomjs-2.x.x-windows folder, open the bin folder, and put phantomjs.exe in %PYTHONFOLDER%\Scripts

3. [You need to sign up here](https://2captcha.com/auth/register)

4. [Verify your email (if needed) and login](https://2captcha.com/auth/login)

5. Either work (Start Work on top) or deposit money (Deposit on left). Get a balance or you will have no credit to solve captchas

6. Click the "2Captcha API" tab at the top

7. Look for captcha KEY. There should be a long string after that like a6ebcb3f4a7b6f6e319d8e1c37e25ec4

8. For the rest of the guide %YOUR_2CAPTCHA_KEY%=the string you found there

## Using Auto-Email Verify
If you want to automatically verify emails, there are some specific instructions you need to follow. To help you understand plusmail, I wrote this snippet.

**To verify all emails while running, refer to Example 8 & 9. You also need to allow less secure apps to connect to your google account because of the python imap library. https://support.google.com/accounts/answer/6010255?hl=en**
~ Thoridal

Also, to verify emails, you should have a relatively empty inbox. Else it needs to index your whole Inbox folder everytime and that isn't very fun.

The PlusMail trick work as follows. Suppose your name is Mark and you own Mark@gmail.com as your email account. If I send an email to Mark+Jacob@gmail.com, it will still go to Mark@gmail.com. Similarly, if I send an email to Mark+asldksdjek@gmail.com, it will go to Mark@gmail.com. The PlusMail trick takes advantage of the fact that Niantic doesn't check that there isn't a difference between Mark and Mark+Jacob because not all email providers support this. When you use "-m mark@gmail", it will generate emails like Mark+asdkjs@gmail.com differently for each account creation, but all emails will go to Mark@gmail.com. To use the plusmail trick, refer to any example with the argument -m

## How to use
Shift+Right Click your desktop and "Open command window here". OR open Terminal if on linux/osx. Note that usernames.txt (the file with the accounts) will be made on your desktop, or wherever you ran terminal/cmd from. To run MonoGen, just type `monogen` into the cmd/terminal. Do not run from C:\ unless you read Example 10. See examples below.

You can type `monogen --help` to see all parameters. Optional parameters are as follows.
```
	--username, -u #This is the username
	--password, -p #This is the password
	--email, -e #This is the email
	--no-plusmail, -n #disable appending username to email address after + sign
	--count, -c #This is the number of accounts to make
	--recaptcha, -r #This is your 2captcha key
	--autoverify, -av #Set this to True if you want to autoverify emails. Otherwise False (or don't use the tag)
	--googlepass, -gp #This is the password to your google account if you are using -m argument and -av True
	--csvfile, -f #This is the location of the output CSV file. Eg: -f 'accounts.csv'
	--startnum, -sn #If you use -c and -u, it will start counting from this number instead
	--captchatimeout, -ct #If you want captcha to timeout of after n seconds	
	--inputtext, -it #If you want to read user:pass from file
	--queue, -q #To automatically add created accounts to a running Monocle instance
```

Example 1 : Create an entirely random account by manually entering the captcha yourself

```
monogen -e 'youremail@domain.com'
```

Example 2 : Create an entirely random account with automated captcha solving

```
monogen -r a6ebcb3f4a7b6f6e319d8e1c37e25ec4 -e 'youremail@domain.com'
(with your own 2Captcha key)
```
	
Example 3 : Create 5 entirely random accounts by manually entering the captcha yourself

```
monogen -c 5 -e 'youremail@domain.com'
```
	
Example 4 : Create 5 an entirely random accounts with automated captcha solving	

```
monogen -c 5 -r a6ebcb3f4a7b6f6e319d8e1c37e25ec4 -e 'youremail@domain.com'
```

Example 5 : Create 5 random accounts that have the same set password=PaSsWoRd by manually entering captcha

```
monogen -c 5 -p PaSsWoRd -e 'youremail@domain.com'
```

Example 6 : Create 1 account that has a specific username=UsErNaMe with automated captcha solving

```
monogen -u UsErNaMe -r a6ebcb3f4a7b6f6e319d8e1c37e25ec4 -e 'youremail@domain.com'
```

Example 7 : Create 5 accounts and add them to a running Monocle instance

```
monogen -c 5 -e 'youremail@domain.com' -q
```

Example 8 : Create 5 accounts using the plusmail trick with email verification and automated captcha solving

```
monogen -c 5 -e emailaddress@gmail.com -r a6ebcb3f4a7b6f6e319d8e1c37e25ec4 -av True -gp GoOgLePaSs
```

Example 9 : Specify the location to save the username:password. By default, it will save in the directory you run cmd/terminal from

```
monogen -f "C:\Users\YoUr_UsEr\Desktop\accounts.csv" -e emailaddress@gmail.com
You need to run cmd as admin if you want to save in C:\
```

Example 10 : Creating multiple accounts with the same username + a number that increments by 1 starting at 15
```
monogen -u user -c 10 -sn 15 -e emailaddress@gmail.com
this will create user15, user16, ..., user 24
```

Example 11 : If it takes longer than 40 seconds to solve captcha, cancel the request and forfeit $0.003
```
monogen -ct 40 -r a6ebcb3f4a7b6f6e319d8e1c37e25ec4 -e emailaddress@gmail.com
```

Example 12 : Read user:pass from a file. It should be formatted like so
```
mark:pass1
jacob:pass2
james:passn
```
```
monogen -it C:\user\sri\desktop\inputaccs.txt -e emailaddress@gmail.com
```

	  
## Common Issues
Please let us know what your issue is, instead of just saying it doesnt work. Copying the error code you receive is very helpful.

- Cannot find chrome binary. Chrome should be installed to the default directory in C. Ensure that it is. If it is, try uninstalling and reinstalling.

- Chromedriver not found. Your chromedriver.exe file is either not in %PYTHONFOLDER%\scripts OR you did put the file there but you do not have an environment path setup for %PYTHONFOLDER%\scripts

- pip is not recognized as an internal or external command. You do not have an environment path setup for %PYTHONFOLDER%\scripts OR python 3.6 is not installed

- git is not recognized as an internal or external command. You did not install GIT

- selenium not found `pip3 install selenium`

- Stuck on processing mailbox. Your mailbox is too populated. The script is going through each email finding the pokemon ones.

## Links
- Google Chrome https://www.google.com/chrome/

- Python 3.6 https://www.python.org/downloads/release/python-360/

- Git https://git-scm.com/download/win

- Download Chromedriver https://sites.google.com/a/chromium.org/chromedriver/downloads

- 2 Captcha Signup https://2captcha.com/auth/register

- 2 Captcha login https://2captcha.com/auth/login

- Email verify script by Sebastienvercammen https://gist.github.com/sebastienvercammen/e7e0e9e57db246d7f941b789d8508186
