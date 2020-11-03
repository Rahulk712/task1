Task #2

###Pulling the Image from docker hub repository
FROM    centos:7
###updating the packages ## default config ...###
RUN yum -y update
###installing the apache packages
RUN yum install -y httpd httpd-tools
###installing some basic packages
RUN yum install -y lynx wget rsync vim bash-completion curl unzip net-tools
###Exporting the port to the externel
EXPOSE  80
###Creating the new ssh user for accessing the application
RUN adduser user1
RUN adduser user2
RUN adduser user3
###Directory Environment for project
RUN mkdir -p /home/user1/{backup,public_html,logs,tmp}
RUN mkdir -p /home/user2/{backup,public_html,logs,tmp}
RUN mkdir -p /home/user3/{backup,public_html,logs,tmp}
###Sample test file for testing the environment
RUN touch /home/user1/public_html/index.html
RUN touch /home/user2/public_html/index.html
RUN touch /home/user3/public_html/index.html
###adding the content to the sample file
RUN echo "this is the test page for test1.azure.com site......." > /home/user1/public_html/index.html
RUN echo "this is the test page for test2.azure.com site......" > /home/user2/public_html/index.html
RUN echo "this is the test page for test3.azure.com site......." > /home/user3/public_html/index.html
###changing the ownership of the directories
RUN chown -R user1:user1 /home/user1/*
RUN chown -R user2:user2 /home/user2/*
RUN chown -R user3:user3 /home/user3/*
###changing the permissions of the project directory
RUN chmod -R 755 /home/*
RUN chmod -R 775 /home/user1/public_html
RUN chmod -R 775 /home/user2/public_html
RUN chmod -R 775 /home/user3/public_html
###customizing the httpd configuration file for multiple projects ##default config....###
RUN sed -i 's/DirectoryIndex index.html/DirectoryIndex index.html index.php/g' /etc/httpd/conf/httpd.conf
###adding the one line space to the httpd configuration file ###default config..###
RUN echo " " >> /etc/httpd/conf/httpd.conf
####### Cross origin Enabled ###### Default config..######
RUN echo "## Cross Origin Enabled" >> /etc/httpd/conf/httpd.conf
RUN echo 'Header set Access-Control-Allow-Origin "*"' >> /etc/httpd/conf/httpd.conf
RUN echo 'Header set Access-Control-Allow-Headers "Origin, X-Requested-With, Content-Type, Accept"' >> /etc/httpd/conf/httpd.conf
RUN echo " " >> /etc/httpd/conf/httpd.conf
RUN echo "KeepAlive on" >> /etc/httpd/conf/httpd.conf
RUN echo "KeepAliveTimeout 7" >> /etc/httpd/conf/httpd.conf
RUN echo " " >> /etc/httpd/conf/httpd.conf
RUN echo "##################################" >> /etc/httpd/conf/httpd.conf
###this is the virtual host configuration for the projects  ### Default config...###
RUN echo "<VirtualHost *:80>" >> /etc/httpd/conf/httpd.conf
RUN echo "DocumentRoot /var/www/html" >> /etc/httpd/conf/httpd.conf
RUN echo "ServerName <server-ip>" >> /etc/httpd/conf/httpd.conf
RUN echo "</VirtualHost>" >> /etc/httpd/conf/httpd.conf
###################################################################################
###enabling the user home directory for the project ###default config...####
RUN sed -i 's/AllowOverride FileInfo AuthConfig Limit Indexes/#    AllowOverride FileInfo AuthConfig Limit Indexes/g' /etc/httpd/conf.d/userdir.conf
RUN sed -i 's/Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec/AllowOverride all/g' /etc/httpd/conf.d/userdir.conf
RUN sed -i 's/Require method GET POST OPTIONS/Require all granted/g' /etc/httpd/conf.d/userdir.conf
RUN sed -i 's/UserDir disabled/# UserDir disabled/g' /etc/httpd/conf.d/userdir.conf
RUN sed -i 's/#UserDir public_html/UserDir public_html/g' /etc/httpd/conf.d/userdir.conf
##################### test1.azure.com ##########################
RUN touch /etc/httpd/conf.d/doctest.conf
RUN echo "##### test1.azure.com ###########" >> /etc/httpd/conf.d/doctest.conf
RUN echo "<VirtualHost *:80>" >> /etc/httpd/conf.d/doctest.conf
RUN echo "       DocumentRoot    /home/user1/public_html" >> /etc/httpd/conf.d/doctest.conf
RUN echo "       ServerName      test1.azure.com" >> /etc/httpd/conf.d/doctest.conf
RUN echo "       ErrorLog        /home/user1/logs/doctest-error_log" >> /etc/httpd/conf.d/doctest.conf
RUN echo "       TransferLog     /home/user1/logs/doctest-access_log" >> /etc/httpd/conf.d/doctest.conf
RUN echo "</VirtualHost>" >> /etc/httpd/conf.d/doctest.conf
RUN echo "######################" >> /etc/httpd/conf.d/doctest.conf
##################### test2.azure.com ##########################
RUN touch /etc/httpd/conf.d/doctest1.conf
RUN echo "##### test2.azure.com ###########" >> /etc/httpd/conf.d/doctest1.conf
RUN echo "<VirtualHost *:80>" >> /etc/httpd/conf.d/doctest1.conf
RUN echo "       DocumentRoot    /home/user2/public_html" >> /etc/httpd/conf.d/doctest1.conf
RUN echo "       ServerName      test2.azure.com" >> /etc/httpd/conf.d/doctest1.conf
RUN echo "       ErrorLog        /home/user2/logs/doctest1-error_log" >> /etc/httpd/conf.d/doctest1.conf
RUN echo "       TransferLog     /home/user2/logs/doctest1-access_log" >> /etc/httpd/conf.d/doctest1.conf
RUN echo "</VirtualHost>" >> /etc/httpd/conf.d/doctest1.conf
RUN echo "######################" >> /etc/httpd/conf.d/doctest1.conf
##################### test3.azure.com ##########################
RUN touch /etc/httpd/conf.d/doctest2.conf
RUN echo "##### test3.azure.com ###########" >> /etc/httpd/conf.d/doctest2.conf
RUN echo "<VirtualHost *:80>" >> /etc/httpd/conf.d/doctest2.conf
RUN echo "       DocumentRoot    /home/user3/public_html" >> /etc/httpd/conf.d/doctest2.conf
RUN echo "       ServerName      test3.azure.com" >> /etc/httpd/conf.d/doctest2.conf
RUN echo "       ErrorLog        /home/user3/logs/doctest2-error_log" >> /etc/httpd/conf.d/doctest2.conf
RUN echo "       TransferLog     /home/user3/logs/doctest2-access_log" >> /etc/httpd/conf.d/doctest2.conf
RUN echo "</VirtualHost>" >> /etc/httpd/conf.d/doctest2.conf
RUN echo "######################" >> /etc/httpd/conf.d/doctest2.conf
###apache service running in the foreground ## default config...####
CMD ["/usr/sbin/httpd","-D","FOREGROUND"]
#########################################################################################################
##After this we need to do the port mapping command is as below
##docker run -itd -p <local machine port number>:<container machine port number> <image name/id>

##Ex: docker run -itd -p <ipadress>:9090:80 
