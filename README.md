# s3-bucket-mounting-on-ec2
aws s3 bucket mounting on ec2 by by scripting for amazon linux machine.


#!/bin/bash
yum update all
   
   
   sudo yum install automake fuse fuse-devel gcc-c++ git libcurl-devel libxml2-devel make openssl-devel -y
      git clone https://github.com/s3fs-fuse/s3fs-fuse.git

      cd s3fs-fuse
      ./autogen.sh
      ./configure --prefix=/usr --with-openssl
      make
      sudo make install
      
      which s3fs
     
     touch /etc/passwd-s3fs
    echo -e 'accesskey:secretaccesskey'   > /etc/passwd-s3fs
     sudo chmod 640 /etc/passwd-s3fs
     mkdir /mys3bucket

     s3fs bucket_name -o use_cache=/tmp -o allow_other -o uid=1001 -o mp_umask=002 -o multireq_max=5 /mys3bucket
