phpThumb() plugin for CakePHP
=============================

This CakePHP plugin uses phpThumb() to dynamically generate thumbnails of images.
It is configurable for using with images uploaded with MeioUpload.

Installation
------------

Clone in plugin directory :

    git clone git://github.com/msadouni/cakephp-phpthumb-plugin.git php_thumb

Or download an archive and extract in `plugins/php_thumb`

Configuration
-------------

Create `config/config.php` with the following code :

    <?php
    $config['PhpThumb']['thumbs_path'] = 'thumbs';

Then create `webroot/thumbs` where the thumbs will be stored.
You might want to add that folder to your .gitignore.

MeioUpload configuration
------------------------

This is only if you want to use MeioUpload to take care of the upload part.

You only need the basic MeioUpload configuration to upload the original image,
since all the thumbnails stuff is done dynamically with this plugin.

In your model :

    var $actsAs = array('MeioUpload.MeioUpload' => array('image'));

Add a varchar image field to the model, create `webroot/uploads` with the write
permissions for you webserver, and you're done.
For more information on MeioUpload, check [the github page](https://github.com/jrbasso/MeioUpload).

This plugin works out of the box with the default MeioUpload configuration,
in which images are stored in `webroot/uploads`with a `model/field` structure.

If you use a different folder than `uploads`, then add

    $config['PhpThumb']['meioupload_path'] = 'my-folder';

to `config/config.php`.

Usage
-----

Load the helper in `AppController` or in each controller where you want to use the helper :

    var $helpers = array('PhpThumb.PhpThumb');

### Normal image

In the view, generate the thumbnail :

    $this->PhpThumb->thumbnail('img/image.jpg', array(
        'w' => 100, 'h' => 100, 'zc' => 1
    ));

In the `$options` array you can use any valid phpThumb() option. For detailed
information on the available options, check [phpThumb()'s readme](http://phpthumb.sourceforge.net/demo/docs/phpthumb.readme.txt)

### MeioUpload'ed image

    // for a Post with an image field containing my-post.jpg
    $this->PhpThumb->thumbnail($post['Post']['image'], array(
        'model' => 'Post', 'field' => 'image', 'w' => 100, 'h' => 100, 'zc' => 1
    ));
    // will render a thumbnail for this post image in /uploads/post/image/my-post.jpg

This will also work :

    $this->PhpThumb->thumbnail('uploads/post/image/.$post['Post']['image'], array(
        'w' => 100, 'h' => 100, 'zc' => 1
    ));
