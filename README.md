# CakeS3 Plugin for CakePHP 2.0

The CakeS3 plugin for CakePHP allows easy integration with an Amazon S3 instance to be dropped into your app.  

Utilising [tpyo's](https://github.com/tpyo/amazon-s3-php-class) amazon-s3-php-class, which in his words is..

> This class is a standalone Amazon S3 REST implementation for PHP 5.2.x (using CURL), that supports large file uploads and doesn’t require PEAR.

This means it can be dropped in and run on a variety of hosting platforms.

## Installation

Do one of the following to use this plugin in your CakePHP 2.0 app

	git clone https://fullybaked@github.com/fullybaked/CakeS3.git app/Plugin/CakeS3
	
or

	git submodule add https://fullybaked@github.com/fullybaked/CakeS3.git app/Plugin/CakeS3
	
or

Just download the package and unzip it into your app/Plugin directory


Then remember to add the following to your Config/bootstrap.php

	//Add the CakeS3 plugin
	CakePlugin::load('CakeS3');

## Setup

Add the following to your controller $components instance variable
	
	// in controller components var
	$components = array(
		'CakeS3.CakeS3' => array(
			's3_key' => 'YOUR_AMAZON_S3_KEY',
			's3_secret' => 'YOUR_AMAZON_S3_SECRET_KEY',
			'bucket' => 'BUCKET_NAME'
		)
	);
	
## Usage
	
List the contents of a bucket

	$contents = $this->CakeS3->list_bucket_contents();
	
List the contents of a path relative to the bucket i.e. a folder	

	$contents = $this->CakeS3->list_folder_contents('path/relative/to/bucket/');
	
Upload a file to S3
	
	$response = $this->CakeS3->put_object('/path/to/local/file', 'path/relative/to/bucket/', [$permission = ACL_PUBLIC_READ]);
	
_Allowed permissions are:_

 * CakeS3::ACL\_PRIVATE
 * CakeS3::ACL\_PUBLIC\_READ
 * CakeS3::ACL\_PUBLIC\_READ\_WRITE
 * CakeS3::ACL\_AUTHENTICATED\_READ
	

Delete a file from S3

	$response = $this->CakeS3->delete_object('path/relative/to/bucket/');
	
Retrieve an object from S3 location

	$object = $this->CakeS3->get_object('path/relative/to/bucket/', [$path_to_store_local_copy = false]);
	
Retrieven information about an object on S3

	$info = $this->CakeS3->get_object_info('path/relative/to/bucket/');
	
Change the bucket name on the fly using method chaining	

	$response = $this->CakeS3->bucket('new_bucket')->{any_of_the_above_methods};

## Features

* List contents of given bucket
* List folder contents within a bucket
* Push files to a location on S3 
* Retrieve an object from S3
* Retrieve information about an object from S3
* Delete files from S3

## Attribution

The S3 php class used by this plugin was developed by [tpyo](https://github.com/tpyo/amazon-s3-php-class)

## Changelog

**Version 0.2 - 6th March 2012**

* Added get_object method
* Added get\_object\_info method
* Made the build\_url\_to\_file method public

## License

Released under the [MIT license](http://www.opensource.org/licenses/MIT).
