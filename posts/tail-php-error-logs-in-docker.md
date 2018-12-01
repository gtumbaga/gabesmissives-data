# Tail PHP error logs in Docker
---

## FIRST - Docker PHP Setup!
Before you can actually see the docker php error logs, you have to enable php error logging in the php.ini file.

I use an Ubuntu php image, and my php.ini location was here:
```bash
/usr/local/etc/php/
```


>  note: if you don't know where your php.ini location is, you can create a *TEMPORARY* php file with this command in it:
>   `<?php phpinfo(); ?>`
>   **REMEMBER** that you should not leave this file existing in your site, because its insecure and will give public access to your server info!


I noticed that my php.ini file didn't exist there, so I had to create it.  Then I added this:
```
log_errors = On
error_log = /dev/stderr
```

<aside class="alert alert-info">(Don't forget to restart the apache, or your container, for the changes to take effect.)</aside>

---

<br><br>
## Tailing the Logs
##### To tail the docker logs, use this command:
```
docker logs -f DOCKER_CONTAINER_NAME
```

#### To tail just the *error* logs:
```
docker logs -f your_php_apache_container >/dev/null
```

#### To tail just the *access* logs:
```
docker logs -f your_php_apache_container 2>/dev/null
```
<br>

---

<br><br>
## Exta Note!
In PHP, you can also use the error logs as a debug console.  Send info to it with:
```
<?php
  error_log('debug message goes here');
?>
```

<br>

---

<br><br>
sources:
- https://github.com/docker-library/php/issues/212
- 
