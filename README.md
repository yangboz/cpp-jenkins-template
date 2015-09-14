# Jenkins Cpp template

With "CppCheck+CppLint+CppNCSS+SLOC+CLOC+Deploy+Email" process.

Use these files to scaffold your Continuous Integration Server within your C++ projects.

This was inspirated by [the PHP jenkins template project](http://jenkins-php.org/) ([github](https://github.com/sebastianbergmann/php-jenkins-template)) by Sebastian Bergmann.

## Overview

![Jenkins-Cpp-Overview](https://raw.githubusercontent.com/yangboz/cpp-jenkins-template/master/Jenkins-cpp-overview.jpg "Jenkins-Cpp-Overview") 

## Requirements

On your jenkins instance, you must install some QA python tools:

* [CppCheck](https://github.com/danmar/cppcheck)

        $ cppcheck --enable=all --inconclusive --xml --xml-version=2 ${WORKSPACE}/SOURCE_FOLDER 2> ${WORKSPACE}/OUTPUT_FOLDER/cppcheck.xml
        
* [CppLint](https://github.com/danmar/cppcheck)

        $ python /home/jenkins/cpplint-all.py ${WORKSPACE}/SOURCE_FOLDER/ 2>&1 | tee ${WORKSPACE}/OUTPUT_FOLDER/cpplint-result.xml    
        
* [sloccount](https://wiki.jenkins-ci.org/display/JENKINS/SLOCCount+Plugin)

        $ sloccount --duplicates --wide --details ${WORKSPACE}/SOURCE_FOLDER > ${WORKSPACE}/OUTPUT_FOLDER/sloccount.sc  
* [cloc](https://wiki.jenkins-ci.org/display/JENKINS/SLOCCount+Plugin)

        $ cloc --by-file --xml --out=${WORKSPACE}/SOURCE_FOLDER/cloc.xml ${WORKSPACE}/OUTPUT_FOLDER
        
* [CppNCSS](http://cppncss.sourceforge.net/)

        $ cppncss [options] [file [file2 [directory [directory2] ...]]]

## Jenkins Plugins

You also need to install some plugins in your jenkins server:

* [Jenkins SLOCCount Plug-in](http://wiki.jenkins-ci.org/display/JENKINS/SLOCCount+Plugin)
* [Jenkins xUnit plugin](http://wiki.jenkins-ci.org/display/JENKINS/xUnit+Plugin)
* [Jenkins Violations plugin](http://wiki.jenkins-ci.org/display/JENKINS/Violations)
* [Warnings Plug-in](https://wiki.jenkins-ci.org/display/JENKINS/Warnings+Plugin)
* [Cobertura plugin](https://wiki.jenkins-ci.org/display/JENKINS/Cobertura+Plugin)


## Jenkins configuration

Install the hudson.plugins.warnings.WarningsPublisher.xml file on the jenkins server, then reload the configuration.

Or, if you prefer to click in the web interface:

1. Go to Manage Jenkins -> Configure System
2. Scroll down to Compiler Warnings -> Parsers
3. Add a new parser(CppLint) with the following details:



## Using the Job Template

1. Check out the `cpp-jenkins-template` project from Git:

        cd $JENKINS_HOME/jobs
        git clone git://github.com/yangboz/cpp-jenkins-template.git cpp-jenkins-template
        chown -R jenkins:nogroup cpp-jenkins-template/

2. Reload Jenkins' configuration, for instance using the Jenkins CLI:

        java -jar jenkins-cli.jar -s http://<jenkins_address>:<jenkins_port> reload-configuration

3. Click on "New Job".

4. Enter a "Job name".

5. Select "Copy existing job" and enter "python-template" into the "Copy from" field.

6. Click "OK".

7. Disable the "Disable Build" option.

8. Fill in your "Source Code Management" information.

9. Configure a "Build Trigger", for instance "Poll SCM".

10. Click "Save".


## In your project

Get the `Makefile` and adapt it (source directory, tasks). Make sure to generate the right files (or change the jenkins config):

* cppcheck.xml

You can also adapt your `.gitignore` file, in order to avoid to commit the generated files.


## Some other resources

* 


## License

(The MIT License)

Copyright (c) 2012 Bertrand Tornil <youngwelle@gmail.com>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

# References:

http://xinsuiyuer.github.io/blog/2014/02/24/jenkins-c-plus-plus-ci-env/
