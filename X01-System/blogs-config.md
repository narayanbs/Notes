##### Configure devenv and notes blogs

* cd Downloads
* git clone https://github.com/narayanbs/blogs
* mkdir myblogs
* cd myblogs
* hugo new site devenv
* cp -r ../blogs/devenv/ .
* cd devenv
* unzip ../../blogs/theme/minimal-bootstrap-hugo-theme.zip -d themes/
* hugo -D server
* You can access the site at localhost:1313/

-----------
Now do the same for notes

* cd ~/Downloads/myblogs
* hugo new site notes
* cp -r ../blogs/notes/ .
* cd notes
* unzip ../../blogs/theme/minimal-bootstrap-hugo-theme.zip -d themes/
* hugo -D server
* You can access the site at localhost:1313/


