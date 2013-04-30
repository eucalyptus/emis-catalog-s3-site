EMIs Catalog on S3
====================

This is the directory layout of all the files associated with http://emis-catalog.s3.amazonaws.com/index.html.  In order to add an image to be accessed on http://emis-catalog.s3.amazonaws.com/index.html, do the following:

* Clone emis-catalog-s3-site:

```
git clone https://github.com/eucalyptus/emis-catalog-s3-site.git
```

* Make sure image is in a tar-gzipped file that has the following layout:

```
* image file (needs to end with .img)
* kvm-kernel folder
  * ramdisk (contains one of the following: initr(d|amfs) or loader in the name)
  * kernel (contains vmlinu in the name)
```

* Open up the catalog-web file and add in a section for the image to be accessed:

```
{
      "url": "<S3 Bucket URL or HTTP URL to tar-gzipped image; if its in an S3 Bucket, make sure the ACLs are set to public>",
      "recipe": "<distro base of image - i.e. centos-based, ubuntu-based, debian-based, etc.>",
      "contact": "<email address of person maintaining the email>",
      "stamp": "<custom stamp created by the following command: date +%s|md5sum|sed '1,$ s/\(....\)\(....\).*/\1-\2/'>",
      "version": "experimental-images",
      "architecture": "<either x86_64, i386 or i686>",
      "single-kernel": "False",
      "hypervisors-supported": ["kvm"],
      "date": "<image date: created by the following command: date "+%Y%m%d%H%M%S">",
      "os": "<os type: for example 'centos', 'debian', 'ubuntu'>",
      "description": "<description of the image; typically has OS type, root filesystem size, kernel/ramdisk version>"
    },
```

* <i>(Optional - Extra Credit)</i> <a href="http://www.eucalyptus.com/docs/3.2/cli/eustore-install-image.html#eustore-install-image">Upload local tar-gzipped file using eustore</a> to a Eucalyptus cloud, and run eutester case to confirm that the image is valid.  For more information, please check out the <a href="https://github.com/eucalyptus/image-verification-results.git">eucalyptus/image-verification-results repo</a>. <i><b>Note:</b> If there is a desire to use the <a href="https://communitycloud.eucalyptus.com/">Eucalyptus Community Cloud</a>, please contact the <a href="mailto:ecc-administrator@eucalyptus.com">ECC Administrator</a> in order to upload the kernel and ramdisk needed for the image.</i>

* Submit a pull request to eucalyptus/emis-catalog-s3-site repo. (We will update http://emis-catalog.s3.amazonaws.com/index.html after the pull request has been merged).



