Mojolicious on OpenShift
========================

Mojolicious framework quick start repo for RedHat OpenShift PaaS.

This repository helps you get up and running quickly with a full Mojolicius installation 
on OpenShift. The recipe is a modification and improvement on 
[mojolicious-lite-openshift](https://github.com/degtyarev-dm/mojolicious-lite-openshift) 
by Dmitry Degtyarev.

Feel free to change it as needed.

Running on OpenShift
----------------------------

Create an account at http://openshift.redhat.com/

Create a perl-5.10 application

    rhc app create -a mojoapp -t perl-5.10

Add this upstream mojolicous repo to your application and generate Mojolicious app

    cd mojoapp
    git remote add upstream -m master https://github.com/tmiklas/mojolicious-openshift.git
    git fetch -q upstream && git merge -q upstream/master
    git rm .htaccess index.pl LICENSE README.md

Now it's time to bring in some Mojolicious code. In this example an empty application skeleton will be 
generated and added to the repo. Please note we remove the top level directory (mojo_app) that contains 
our application:

    mojo generate app MojoApp
    cd mojo_app && mv * ../ && cd .. && rmdir mojo_app
    touch log/.gitignore
    git add script lib t log public templates
    git commit -a -m "added basic scaffolding"
    
The .htaccess file is automaticlly generated for your application during the deployment process so it is not 
included in the source control.

The final step is to push the code to OpenShift:

    git push

That's it, you can now checkout your application at:

    http://mojoapp-$yournamespace.rhcloud.com

**Credits**
[Dmitry Degtyarev](https://github.com/degtyarev-dm)
