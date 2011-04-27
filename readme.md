# phpThumb Plugin for CakePHP #

CakePHP plugin with phpThumb library and helper to generate thumbnails.

## How to use the helper ##

Create a directory "php_thumb" in your app/plugins folder. Clone/copy the plugin in the app/plugins/php_thumb folder. 

Load the phpThumb helper in each controller where you want to use the helper:

	var $helpers = array('PhpThumb.PhpThumb');
	
You can use it in your view as follows:

	<?php
    $thumbnail = $this->PhpThumb->generate(
        array(
        	'save_path' => WWW_ROOT . 'assets/img/thumbs',
        	// Where to save the thumbnail. (Make sure it is writable by the web server)
        	'display_path' => '/assets/img/thumbs',
        	// The web accessible path to the directory that the thumbnail lives in after its created.
        	'error_image_path' => '/assets/img/error.jpg',
        	// The default image to display if something goes wrong while generating a thumbnail. 
    		'src' => WWW_ROOT . 'assets/img/srcImage.jpg',
    		// The source image to be converted into a thumbnail.
    		// From here on out, you can pass any standard phpThumb parameters
    		'w' => 100, 
    		'h' => 100,
    		'q' => 100,
    		'zc' => 1
        )
    );
   	echo $this->Html->image($thumbnail['src'], array('width' => $thumbnail['w'], 'height' => $thumbnail['h']));
   	?>

## Fork ##

The helper has been forked from https://github.com/DanielMedia/phpThumb-Helper
More info at http://daniel-salazar.com/post/1/phpthumb-helper-for-cakephp

## phpThumb library ##

Currently installed version is 1.7.9. Go to http://phpthumb.sourceforge.net for more information.


