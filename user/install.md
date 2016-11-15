---
layout: doc
title: Installation
---

# Installation

The NetworkCurator is free software and is available from github. To create an instance of the NetworkCurator and manage your own networks, you will have to download and configure the software on a web server.

This chapter provides an installation tutorial divided into the following parts

- [Web server setup](#hosting): covers prep of a hosting account for the installation
- [Installation of core software](#nccore): covers download and configuration of the server-side software
- [Installation of the web interface](#ncui): covers download and configuration of the user interface
- [Updating the software](#ncupdates): covers how to update the software
- [Appendix](#ncappendix) - covers some topics left out of the main tutorial

The tutorial assumes that you already have a web domain and a hosting account from a commercial provider. In the examples, we will assume that the domain is `sitename.org` and the administrator account for the site is `siteadmin`. The code snippets assume a linux-based environment.



<a name="hosting"></a>

## Web server setup

The first stage of the installation is setting up a database on your web server. The database will be used to store user and network data.

Unfortunately, hosting providers provide different features and interfaces, making it impossible to provide precise step-by-step setup instructions. However, setting up a database requires only a few steps and can be performed through the graphical control panel provided through a hosting package. 

1. Log in to your hosting control panel. Such control panels often have a  toolbar on the left side and groups of icons on the right side.

2. Find the section of the control panel that refers to databases. Find an icon marked 'MySQL Databases' or that otherwise promises to `create a new database`. Click that icon and you should see a new screen with a form and various options. 

3. Follow the instructions on the `create database` screen. You will need to enter a name for your database. It will be convenient to name the database `networkcurator` (all lowercase, no spaces). Click `OK` or equivalent button to create the database. 

4. Next, we will need to create database user accounts. These accounts are needed to enable the NetworkCurator software to access and modify the contents of the database. 

    Go back to the database page. Find the section that promises to 'add new users'. Create two new accounts named `nc_admin0` and `nc_admin1`. For each, choose a strong password for each account and write it down in a secure place.

5. We now must connect the user accounts with our database. On the database page, find the section that promises to 'add users to database'. For each account `nc_admin0` and `nc_admin1`, connect the user to the `networkcurator` database. If during this process the page asks about user privileges, you should assign 'ALL PRIVILEGES' to both users.

6. Database user accounts can be configured with various permissions levels. We will need our users to have full access to the `networcurator` database. If the process in the previous step did not already ask about privileges, find the relevant section on the database page and select `Grant all privileges` or equivalent to the two users.


The web server and database setup is complete. If you would like to verify your actions, look for an icon in the control panel called `phpmyadmin`. Click that icon and you should see a page providing some information on your databases, which should now include `networkcurator`. 


<a name="nccore"></a>

## Installation of the server-side software

The next stage of the installation involves downloading the NetworkCurator software and configuring it on the web server. This software is necessary in order to interact with the database created above. 

The following instructions describe a clean installation using a git clone. This strategy copies the current version of the software onto the web server and also establishes a relationship between the install instance and the github source. We will later use this relationship to update the software in a later section.

 1  We start the installation from a shell on your local computer. Connect to the web server via ssh. Enter command

    ```
    ssh siteadmin@sitename.org
    ```

    Provide your password when prompted. 

 2  The connection to the server likely lands you in your home directory. Navigate to the directory that is dedicated to public (i.e. www) pages. This is often called `public_html`. 

  ```
  cd public_html
  ```

 3  We now have to choose an installation directory. If the entire site will be dedicated to the NetworkCurator, the current directory (i.e. `public_html`) is the installation directory. If the NetworkCurator is only a part of a larger site, create or navigate to the intended location.

 4  We will need the installation directory to be empty. To check this, execute 

    ```
    ls
    ```
 
    This command should display nothing, or only files that are truly redundant (we will delete them shortly). An `index.html` or `index.php` that comes with a hosting package is redundant. So is a directory `cgi-bin`. Items called `./` or `../` are ok too. If there are any such existing files, we will now delete them

    ```
    rm -r *
    ```

 5  We are now ready to download the NetworkCurator software. We will do this by cloning using the following command (note the dot at the end, it's important!)

    ```
    git clone https://github.com/tkonopka/NetworkCurator.git .
    ```

    You should see some progress messages while the files are copied. Once the process is complete, we can inspect the new contents of the directory

    ```
    ls
    ```

  This should list a number of directories and files. In particular, there should be a file `index.php` and several directories starting with the prefix `nc`.

 6  We now have to configure the software, i.e. enable interactions with the database. There is configuration file to do this in the `nc-admin/install` directory. We thus navigate there

    ```
    cd nc-admin/install
    ls
    ```

    The second command should list files `install-settings.php` and `install.php`. These files contain core settings that apply to the software as a whole. But we need to specify settings that are specific to our `sitename` installation. To do this, we need to create a new file called `install-settings-local.php` using a text editor. Execute the following command:

    ```
    nano install-settings-local.php
    ```

    This should open a blank area where you can type-in some text. Enter the following defintions

    ~~~ php
    <?php
    define("DB_ROOT_PASSWD", "curating#networks4science");
    define("DB_ADMIN_PASSWD", "another1001#SCIadventures");
    define("NC_APP_ID", "sitename");
    define("SERVER", "sitename");
    define("NC_PATH", "");
    define("NC_SITE_NAME", "sitename");
    define("NC_SITE_ADMIN_PASSWORD", "adminpassword");
    ?>
    ~~~

  Each line consists of a `define` statment, a name in uppercase letters, and a value in quotes. Adjust the values in quotes to suit your local installation. 
  
  - make sure the two passwords at the top matche what you used during database setup
  - choose an adequate password for the admin user (last line above)
  - if your installation directory is `public_html`, you can leave the `NC_PATH` as is; if your installation directory is a subdirectory, adjust `NC_PATH` accordingly
  - (Remember to change `sitename` placeholder to your actual domain name)

  After adjustements, save the file and exit (`Ctrl-X`, then `Y`, then `Enter`).


 7  We can now run the installation script. On the command prompt, execute the following command

    ```
    php install.php
    ```

    This command should only take a few moments and generate several lines of messages. All should end with `ok` indicating success.


The core NetworkCurator software is now ready. Next, we will install the user interface.



<a name="ncui"></a>

## Installation of a user interface

In the previous section we configured the server-side software. We now have to install a graphical user interface. In this tutorial we will install the default interface, which is found in another github repository called `NetworkCurator-ui`.

1. If you are continuing from the previous steps, you are now at the command prompt in the directory called `nc-admin/install`. Navigate back to the root of the installation directory (we used `public_html). 

  ```
  cd ../../
  ls
  ```

  The second command should display the same information as we saw earlier, including an `index.php` file. 

2. We now have to create a subdirectory for the user interface. This directory must be called `nc-ui`. Create this folder and navigate inside.

  ```
  mkdir nc-ui
  cd nc-ui
  ```

3. We can now download the user-interface, again using cloning from github. The command is (note the dot at the end)

  ```
  git clone https://github.com/tkonopka/NetworkCurator-ui.git .
  ```

  You should see some progress messages while the files are copied. If you like, you can inspect the contents of the directory using `ls`. Finally, navigate back to the root directory. From the present location, type

  ```
  cd ..
  ```


The user interface should now be ready. We're almost done, only one more step.
  


<a name="ncupdates"></a>

## Updating the software

Open-source software is often a work-in-progress. Some time after you install a version of the software, you might like to update the software to benefit from new features or bug fixes. After a clone-based installation, it is very easy to incorporate such updates into a local NetworkCurator instance. 

Since we installed the server-side and user-interface software separately, we will also have to update these components separately. 

If you are not already logged in to the web server, log in using ssh.

```
ssh siteadmin@sitename.org
```

Navigate to the root directory of your NetworkCurator instance. This might be `public_html`. (If you are continuing the installation from the previous section, you can skip this step)

```
cd public_html
```

To run the update mechanism, execute the following command

```
./pull-update
```

This will replace the software files with the most up-to-date versions from the github repository. All configuration files, database contents, and other files that are specific to your site will not be affected.




<a name="ncappendix"></a>

## Appendix

This appendix contains miscellaneous comments relating to installation and setup. 


### Software requirements

The NetworkCurator software uses MySQL as a database and PHP5.5 as a server-side scripting language. These should already be installed on your web server. However, hosting providers can differ with regard to the default version of PHP. You can identify your version by executing (on the command prompt) 

```
php -version
```

The version number should 5.5 or higher. If it is not, contact your web server administrator or hosting provider.


### SSL encryption

It is standard practice to use SSL encryption to protect private user data such as account details or passwords. It is thus highly recommended that you set up SSL encryption for your web server. The details of this procedure are beyond the scope of this tutorial, but your hosting provider should be able to provide details.

Once SSL is enabled, you should be able to point your browser to an address starting with `https://`. 


