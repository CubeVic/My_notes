## **Initial setup**
![.msi make it easy to install it](img/000.png)

### **Download Jenkins**

Jenkins can be downloaded on:

[Jenkins](https://www.jenkins.io/){: .center}

Jenkins is available for different OS, such as Windows, Mac, and Linux.

There are some hardware pre-requisites:

- 256MB of RAM.
- 1GB of free space ( although according to the documentation 10GB is recommended if one uses the docker container)
- Java
- Web browser (supported Browsers Chrome, Mozilla Firefox, Microsoft Edge, and Apple Safari)

### **Install Jenkins**

On Windows, a `.msi` file will be downloaded which can facilitate the installation.

![.msi make it easy to install it](img/001.png){: .center}

I can run the wizard to install it.

![Jenkins wizard](img/002.png){: .center}

I need to select the logon type (in my case, the option `Run service as LocalSystem` is enough, but in a production 
environment might be better be safe and select the next option)

![Logon Type](img/003.png){: .center}


The last step is to set the port where I will run Jenkins, by default will be `8080`.

![Select the port](img/004.png){: .center}


## ⚠️ Make sure Java is already installed in the system

If everything is correct, I should be able to use the browser to navigate to the [localhost](http://localhost/) 
with the port selected, for example, `http://127.0.0.1:8080` and we will find the Jerking welcome page.

![Unlock Jenkins](img/005.png){: .center}


If this is the first time using this instance of Jenkins, it will ask for a password stored in a specific location.

### **Customize Jenkins**

Jenkins will provide a shortcut to get the plugin if this is the first time I am using this instance

Install suggested plugins

![suggested plugins](img/006.png)![suggested plugins](img/007.png)

For now, I will choose to `Install suggested plugins`

## **Creating the administrator user**

If this is the first time using the instance Jenkins will ask for the creation of an administrator account.

![Create an Administrator account](img/008.png){: .center}


After creating the user, Jenkins will ask couple more questions for the setup, and then it is done.

![Jenkins is ready!](img/009.png){: .center}

### **Installation with `.war` file**

If instead of downloading the installer, I decided to download the `.war` file I need to follow:

1. Navigate to the location of the `.war` file
2. Execute the command `java -jar jenkins.war`

<aside>
☝🏾 It is easier if I navigate to the location of the file using Windows explorer, once in the file location, on the 
top bar I use this will open in that location (check the gif below).

</aside>

![shortcut](img/010.gif){: .center}

1. In this location, I use the command

```
java -jar jenkins.war
```

This will open Jenkins in the default port `8080` however if I want to open it in a different location I can use

```
java -jar jenkins.war --httpPort=(the port I want)java -jar jenkins.war --httpPort=9191
```

![launching Jenkins from the console.](img/011.gif){: .center}

launching Jenkins from the console.

## **Adding the Robot Framework plugin**

Jenkins allows adding a plugin that helps with the automation, in this case, I want to use Jenkins to run the Robot framework test, so I need to install the robot framework plugin

1. Navigate to Manage Jenkins.

![Manage Jenkins](img/012.png){: .center}

2. Locate manage plugins.

![Locate manage plugins](img/013.png){: .center}

3. Switch to the Available tab and search for `robot framework`.

![Plugin Manager](img/014.png){: .center}

4. Check the box and later install without restart.

![Installing plugin](img/015.gif){: .center}


## **How to Create a job in Jenkins**

To create a job I can start by:

1. Navigating to a new item.

![New Item](img/016.png){: .center}

2. Select the Freestyle project

![Freestyle project](img/017.png){: .center}

3. Once on the configuration page, I need to tell Jenkins to execute the test case, 
I can do that using the **built** section and selecting `Executing Windows batch command` if I am running Jenkins in 
windows and `Execute Shell` if I am in Linux or MAC.

![Execute Windows batch Command](img/018.png){: .center}

4. In this space, I need to navigate to the folder where the `.robot` files representing the test case are and run the
`robot command`.

![Build section](img/019.png){: .center}

![build commands](img/020.png){: .center}


5. I need to tell Jenkins where to publish the Framework test results, for that I need to configure the Post-build 
Actions.

6. In the section post-built Actions, select **`Publish Robot Framework test results`**

![Post-Build](img/021.png){: .center}

I can either provide the full path to the directory of Robot Output

![Path to the result folder](img/022.png){: .center}

Path to the result folder

![path to the result folder](img/023.png){: .center}

or I can define a custom workspace and shorten the path.

![Shortcut](img/024.gif){: .center}


## **Run the Robot Framework Job**

Once the job is created and everything is configured I can run the job by clicking on `build now`

![Build Now](img/025.png){: .center}

<aside>
***Before continue***
</aside>

### **Troubleshooting**

The Builds are shown as `failed` but if I inspect the result they say the test passed,

![build](img/026.png){: .center}

![build](img/027.png){: .center}

This is because I made a mistake during the configuration, I have the following

***Step 4 is the build***

```
C:
cd C:\Users\Victo\PycharmProjects\robotframework_twitch\Tests\twitch\FunctionalTestSuite
robot -d Result VideoSearch_Android.robot
```

but `robot -d Result VideoSearch_Android.robot` is not a valid command, and I can prove this by checking the test 
console output

![Console output](img/028.png){: .center}

Console output

Here I can see what the console printed

![console](img/029.png){: .center}

So the test is passing, but due to my mistake of adding a not *recognized internal command*, Jenkins reported it as 
failed.

#### **The solution**

Remove the command `robot -d Result VideoSearch_Android.robot` from step 4.

## **Show HTML reports on Jenkins**

Robot Framework will generate some reports but if I try to see it on Jenkins I will get some errors like this :

![html report](img/030.png){: .center}

So I need to make some small changes

#### **The problem**

There is some issue with the Content Security Policy and by default Jenkins will block the HTML results generated by the Robot framework

[Configuring Content Security Policy](https://www.jenkins.io/doc/book/security/configuring-content-security-policy/)

#### **The solution**

Unset the header, for this, I can use the command

```jsx
System.setProperty("hudson.model.DirectoryBrowserSupport.CSP", "")
```

I need to go to the correct place to paste this command

1. Navigate to the dashboard.
2. Go to manage Jenkins.
3. Look for the option Script console.

![Script console](img/031.png){: .center}

Script console

4. Paste the command here

![Script Console](img/032.png){: .center}

Script Console

<aside>
☝🏾  You will need to run the test again.
</aside>

## **🤖Robot Results**

Now to see the general result and some useful graphics I can go to `robot results`

![Robot Results](img/033.png){: .center}
