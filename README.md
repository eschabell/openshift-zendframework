ZendFramework on OpenShift Express
==================================
Installing the ZendFramework on OpenShift was never easier!

This git repository helps you get up and running quickly w/ a ZendFramework
installation on OpenShift Express. This guide will get you up and running on
ZendFramework-1.11.6-minimal. See Notes at the bottom for steps to pull another
version.


Running on OpenShift
----------------------------

Create an account at http://openshift.redhat.com/

Create a php-5.3 application

    rhc-create-app -l $username -a zendphp -t php-5.3

Add this upstream zendphp repo

    cd zendphp
    git remote add upstream -m master git://github.com/eschabell/openshift-zendframework.git
    git pull -s recursive -X theirs upstream master
    # note that the git pull above can be used later to pull updates to zendphp
    
Then push the repo upstream

    git push

That's it, you can now checkout your application at:

    http://zendphp-$your_domain.rhcloud.com


NOTES:

To install a version of ZendFramework you can follow the steps below.

Download ZendFramework minimal package:

Zip:http://framework.zend.com/releases/ZendFramework-1.11.6/ZendFramework-1.11.6-minimal.zip
Tar:http://framework.zend.com/releases/ZendFramework-1.11.6/ZendFramework-1.11.6-minimal.tar.gz
(Or just go to http://framework.zend.com/download/latest for the latest links)

Create a working directory.

$ mkdir zendframework

Uncompress here and cd into the ZendFramework-1.x.x-minimal directory.

$ cd zendframework

$ unzip|tar xzvf <path to ZendFramework Tarball>

Use the zf.sh script in the bin directory to generate default project

$ [ZendFramework-root]/bin/zf.sh create project zendframework_default

Go back to top level zendframework directory and create our application on OpenShift.

$ cd ../

$ rhc-create-app -l $username -a zendphp -t php-5.3.2

Move the default files into the git repository and push them. The directory
'php' is the document root for PHP applications, so we copy the contents of
the public folder that ZendFramework created in here.

$ cd zendphp

$ cp [path-to]/zendframework/zendframework_default/public/* php/

$ cp -R [path-to]/zendframework/zendframework_default/application .

$ cp -R [path-to]/zendframework/zendframework_default/library .

$ cp -R [path-to]/zendframework/ZendFramework-1.11.6-minimal/library/Zend library/

Add all these files to git repo and push.

$ git add .

$ git commit -m 'Initial import of ZendFramework'

$ git push origin

