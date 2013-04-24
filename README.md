RPM Specs for Logstash on RHEL4
================

This spec has it's origin from Lars Franke,
https://github.com/lfrancke/logstash-rpm
I only tried to adapt the scripts to work on RHEL4

To be able to run logstash on RHEL4 you have to compile it with the 1.6.8-version of JRuby.
I've managed to do that with logstash 1.1.9. I'm not sure if everything is working as it should though.
You should do a "sudo yum groupinstall Development tools" to make sure you have all development tools in place.
Please follow the instructions from CentOS on how to set up a RPM build environment:
http://wiki.centos.org/HowTos/SetupRpmBuildEnvironment


To create a jar file for RHEL4 you have to:

1. Download the source of logstash 1.1.9 from github:

  $>git clone https://github.com/logstash/logstash.git
  <BR>
  $>cd logstash
  <BR>
  $>git checkout v1.1.9
  
2. Edit the Makefile in logstash repository root folder,

  Change the value of<BR> JRUBY_VERSION=1.7.1<BR> to<BR> JRUBY_VERSION=1.6.8
  
3. Build it with

  $>make jar
  
4. move the jar file located in build folder of logstash repo to your ~/rpmbuild/SOURCES
5. From this repo: move SOURCES folder and SPECS folder to ~/rpmbuild
6. rpmbuild -bb ~/rpmbuild/SPECS/logstash.spec
7. take care of your precious rpm located in ~/rpmbuild/RPMS/noarch/
8. Install it on your servers


