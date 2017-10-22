# Wordpress docker image
After start docker compose from `wordpress-stack` using [docker-compose](https://github.com/docker/compose/releases), we should modify the wordpress settings or then commit to new docker image.

This project followed [Quickstart: Compose and WordPress](https://docs.docker.com/compose/wordpress/).


# Troubleshooting
Wordpress limit the size of the upload files, we can create a file named `htaccess`, and add the following content

```
php_value upload_max_filesize 33554432
php_value post_max_size 35651584
php_value memory_limit 37748736
```
where the unit of size is `bytes`.

And then copy this file to docker container `wordpressstack_wordpress_1` which created by image `wordpress:latest`.

```sh
# host
docker cp htacess <container_id>:/var/www/html/

# docker container
mv .htacess .htacess.bak
mv htacess .htacess
```

then we will get large size limit of files.


## Reference
- [Allowed memory size of 262144 bytes exhausted (tried to allocate 24576 bytes)](https://stackoverflow.com/a/16878675)
- [6 Ways To Increase the Maximum Upload File Size in WordPress](https://www.bitcatcha.com/blog/2016/increase-maximum-upload-file-size-in-wordpress/)
