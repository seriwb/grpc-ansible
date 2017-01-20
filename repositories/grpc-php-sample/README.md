PHPでgRPCを利用するサンプル

- 受信と送信
- Phalcon


$ curl -O http://pear.php.net/go-pear.phar
$ sudo php -d detect_unicode=0 go-pear.phar

sudo pecl install grpc

make test


Build process completed successfully
Installing '/usr/local/lib/php/extensions/no-debug-zts-20151012/grpc.so'
install ok: channel://pecl.php.net/grpc-1.0.1
configuration option "php_ini" is not set to php.ini location
You should add "extension=grpc.so" to php.ini
[vagrant@dev-grpc grpc]$ 

sudo vi /etc/php.d/grpc.ini


```
$ cd grpc/src/php/ext/grpc
$ phpize
$ ./configure
$ make
$ sudo make install

Update php.ini

Add this line to your php.ini file, e.g. /etc/php5/cli/php.ini

extension=grpc.so
```


```visudo
Defaults    always_set_home

Defaults    env_reset
Defaults    env_keep =  "COLORS DISPLAY HOSTNAME HISTSIZE INPUTRC KDEDIR LS_COLORS"
Defaults    env_keep += "MAIL PS1 PS2 QTDIR USERNAME LANG LC_ADDRESS LC_CTYPE"
Defaults    env_keep += "LC_COLLATE LC_IDENTIFICATION LC_MEASUREMENT LC_MESSAGES"
Defaults    env_keep += "LC_MONETARY LC_NAME LC_NUMERIC LC_PAPER LC_TELEPHONE"
Defaults    env_keep += "LC_TIME LC_ALL LANGUAGE LINGUAS _XKB_CHARSET XAUTHORITY"

#
# Adding HOME to env_keep may enable a user to run unrestricted
# commands via sudo.
#
# Defaults   env_keep += "HOME"

Defaults    secure_path = /sbin:/bin:/usr/sbin:/usr/bin
```