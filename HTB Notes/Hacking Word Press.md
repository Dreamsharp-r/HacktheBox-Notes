   

Hacking Word Press

Command list  
![c30c82356dccbb0a3a2ce96dd4c07c0e.png](8e2fd9365d624c0bb5104d53c48069df.png)

- Wordpress usually written in php w/ Apache running and MySQL as the backend
    
- After installation, all WP files are located in the var/www/html  
    ![f0d42f7fff8eceaac2c41101c40006af.png](9e72b8bdf9f843459a13621ba12a024f.png)
    
- index.php = homepage of WordPress
    
- license.txt = useful info ex. vs of WP
    
- wp-activate.php = email activation process
    
- wp-admin = login page for admin  
    ![bf06e0ddcab781216916f16222512d31.png](5a60321f62794b908467aaa46f9680bc.png)
    
- wp-config.php = contains information to connect WP to the database  
    ![a5ccae36cb356e7750f8d5ef4d3cb762.png](0c620e58bb2b41c9b33386c273536fba.png)
    
- wp-content = folder where plugins and themes are stored.
    
- wp-includes = contains core files, certificates, fonts JS files, and widgets
    

-Five types of users in WP  
![3c1fc978296922f59d3238300c37027b.png](9e736c1adaa847369ee5bddbe0d7f547.png)

Useful Commands

- curl -s -X GET [http://blog.inlanefreight.com](http://blog.inlanefreight.com "http://blog.inlanefreight.com") | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'wp-content/plugins/*' | cut -d"'" -f2
- Search for plugins
- curl -s -X GET [http://blog.inlanefreight.com](http://blog.inlanefreight.com "http://blog.inlanefreight.com") | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'themes' | cut -d"'" -f2
- Search for themes

Finding the admin user portal  
![7a5f2549243db7c2c57e945cfbdc734d.png](6cb5e3b28fac49ab89d393a1cf7b0418.png)

Using Curl to find via the sh  
![afdfc814ed25d96470b35b705843e18e.png](4bfe296089894a50b066fbfa0f72aef0.png)

Using Curl w/ Json to find users  
![65c39aab43e584772f68715a04e7cc00.png](18f2ba9a2ab84f01bd093f190a0338a5.png)

Listing the available methods to enumerate using xmlrpc.php  
![d30e91ab87b63150b8943e5dd54bd098.png](../_resources/0b0c5638cf6f4cdfb36582d1a6fe3aab.png)