---
title: "How to redirect HTTP to HTTPS Using .htaccess"
datePublished: Sun Nov 25 2018 23:00:00 GMT+0000 (Coordinated Universal Time)
cuid: ck2a1xkxx009k3is1c7jsp9vw
slug: how-to-redirect-http-to-https-using-htaccess
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1586921949665/7Twi5MAFE.png
tags: ssl, programming, security

---

Chrome and Firefox have started showing insecure warnings on sites without [SSL certificates](https://www.instantssl.com/ssl.html). Without SSL, your website
will show insecure to the visitors. Therefore, using an SSL-encrypted connection
for safety, accessibility or PCI compliance reasons is necessary. It becomes
very important to redirect from HTTP to HTTPS.


## What is SSL?

SSL (Secure Sockets Layer) is a standard security protocol for establishing
encrypted links between a web server and a browser in online communication.

The usage of SSL technology ensures that all data transmitted between the web
server and browser remain encrypted.

An **SSL certificate** is necessary to create an SSL connection. You would need to
give all details about the identity of your website and your company as and when
you choose to activate SSL on your web server. Following this, two cryptographic keys are created with a Private Key and a Public Key.

[Learn More: Why SSL is
Critical?](https://www.sslrenewals.com/blog/why-is-ssl-important-benefits-of-using-ssl-certificate)

In order to force your web traffic to use HTTPS, edit the codes in the
**.htaccess file.**

Before we move onto redirecting HTTP to HTTPS, here's how you can edit .htaccess
file. If you already know skip to Redirection steps.

## Editing .htaccess File

There are instructions/directives in the .htaccess file that tell the server how
to act in certain scenarios and directly affects how your website functions.
Common directives in .htaccess file:

* Redirects
* Rewriting URLs

**Ways to edit a .htaccess file:**

-  Edit the file on your computer and upload it to the server using FTP.
-  Use "Edit" mode in the FTP program that allows you to edit a file remotely.
-  Use a text editor and SSH to edit the file.
-  Use the File Manager in **cPanel** to edit the file.

## Editing .htaccess in cPanel File Manager

**Note:** Backup your website in case something goes wrong.

-  Login to cPanel
-  Files > File Manager > Document Root for:
-  Now select the domain name you want to access
-  Check "Show Hidden Files (dotfiles)"
-  Click "Go"
-  After a new tab or window opens, look for the .htaccess file.
-  Right-click on the .htaccess file and click on "Code Edit" on the menu.
-  A dialogue box may pop up asking about encoding. Click the "Edit" button to
continue.
-  Edit the file
-  "Save Changes" when done.
-  Test your website to make sure it is done correctly. In case, there is an error,
restore to the previous version and try again.
-  Once you are done, click "Close" to close the window.

## Redirecting HTTP to HTTPS

### 1. Redirect All Web Traffic

If you have existing code in your .htaccess, add the following:

```
RewriteEngine On
RewriteCond %{SERVER_PORT} 80
RewriteRule ^(.*)$ 
```

### 2. Redirect Only a Specific Domain

For redirecting a specific domain to use HTTPS, add the following:

```
RewriteEngine On
RewriteCond %{HTTP_HOST} ^yourdomain\.com [NC]
RewriteCond %{SERVER_PORT} 80
RewriteRule ^(.*)$ 
```

### 3. Redirect Only a Specific Folder

Redirecting to HTTPS on a specific folder, add the following:

```
RewriteEngine On
RewriteCond %{SERVER_PORT} 80
RewriteCond %{REQUEST_URI} folder
RewriteRule ^(.*)$ 
```

> NB: Replace **"yourdomain"** with your actual domain name wherever required.
Also, in case of the folder, replace **/folder** with the actual folder name.

---

Think it was helpful? Share this article to help others come on HTTPS :).

