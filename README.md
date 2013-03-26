# codeigniter-facebook-lib

A library for quickly integrating Facebook into codeIgniter 2

This repository can be used as is or can be installed as a git submodule for your project.

At this moment, this library is very simple, it basically makes the facebook-PHP-SDK work inside 
CodeIgniter with a nice and easy interface.

This project does actually contain the facebook-php-sdk in it - later I'll probably remove these files and add them as submodules, but for now, that's what we've got.
I will be working over time on the project, creating facilitators for the commonly used facebook-api calls in order to 
simplify development. A point for thoes who might worry about destructive changes to the code-base.

I am using this code in a couple of production sites, hence I will not be tweaking things that can cause a break on the code.
I am not responsible for Facebook updates to it's API, but whenever they do, I'll try to be quick in updgrading the code.
I am accepting pull requests, but they must, at all times, either implement new features or be backwards compatible.
Well, I guess that's all for the intro. Have fun and please let me know if you are using this code or run into any trouble.


##Cloning the repo

###Just a clean single time clone
Clone this into your codeigniter app in the directory
/application/libraries/facebook
with the command:

<pre lang="bash">
git clone https://github.com/bugzbrown/codeigniter-facebook-lib.git facebook
</pre>

This should create a directory facebook in your libraries.

###Adding it as a git submodule
Git submodules are very handy for this kind of thing - It allows you to keep up to date with the lates versions of your 
favourite modules. There are some **bewares**, never the less, I tend to use this approach for my development.
If your project is already using git, you can add the facebook library as a module.
Go to the root of your code igniter app, type in the following:
<pre lang="shell">
git submodule add https://github.com/bugzbrown/codeigniter-facebook-lib.git application/libraries/facebook
</pre>

You can, whenever ther is an update for this specific module, update it automatically by issuing the following git command:
<pre lang="shell">
git submodule update
</pre>

##Configuring
Best practices suggests that you create environment aware config files. These are all based off the "facebook.config.php" file located in the folder.

If you are using environemnt configs, copy this file to your **development** and **production** folders with as **facebook.php**

<pre lang="shell">
cp application/libraries/facebook/facebook.config.php application/config/development/facebook.php
cp application/libraries/facebook/facebook.config.php application/config/production/facebook.php
</pre>

If you don't use env configs, just copy the file to your config folder:

<pre lang="bash">
cp application/libraries/facebook/facebook.config.php application/config/facebook.php
</pre>

Edit the file according to your facebook app.

You can load the library wherever you need it and it should just simply work.

##Usage

###Load the library:
You can load the library on a method by method basis or you can add it to the constructor for a controller or even add it to the autoload file.
<pre lang="php">
$this->load->library('facebook/fb');
</pre>

###Initialize the Facebook Object
In any of your controllers you can initialize the facebook object like this:
<pre lang="php">
$this->fb->init_facebook();
</pre>
This will automatically check to see if the user is logged and authenticated with your app, if he is not, it will do the authentication thingy with facebook, and redirect the user back to the canvas page.

Once the user is authenticated, it will create a couple of necessary objects that can be used:

### The user FBID:
<pre lang="php">
echo $this->fb->user;
</pre>

###The Graph API Method:

<pre lang="php">
$profile = $this->fb->api('/me','GET')
echo $profile['name'];
</pre>

###The FQL method:
<pre lang="php">
$retval = $this->fb->fql('SELECT name FROM user WHERE uid = '. $this->fb->user);
echo $retval[0]['name'];
</pre>

### The Logout URL:

<pre lang="php">
echo '&lt;a href="' . $this->fb->logout_url . '">Logout&lt;/a>';
</pre>


## Replacing the Facebook SDK
Facebook is quite active with it's SDK, usually releasing a new version every copuple of months. I will try to keep the module
up to date with the latest stable release of the SDK, but, in case you need to upgrade (assuming you can't run git on your server or something like that),
all you need to do is copy the files in the **src** directory in the <a href="https://github.com/facebook/facebook-php-sdk">facebook-php-sdk</a> to the folder **fb-php-sdk**.

