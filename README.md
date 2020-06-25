## Sensu-Plugins-php-fpm

[![Gem Version](https://badge.fury.io/rb/sensu-plugins-php-fpm-boutetnico.svg)](https://badge.fury.io/rb/sensu-plugins-php-fpm-boutetnico.svg)
[![Sensu Bonsai Asset](https://img.shields.io/badge/Bonsai-Download%20Me-brightgreen.svg?colorB=89C967&logo=sensu)](https://bonsai.sensu.io/assets/boutetnico/sensu-plugins-php-fpm)

## This is an unofficial fork

This fork is automatically tested, built and published to [RubyGems](https://rubygems.org/gems/sensu-plugins-php-fpm-boutetnico/) and [Bonsai](https://bonsai.sensu.io/assets/boutetnico/sensu-plugins-php-fpm).

## Files
 * bin/check-php-fpm.rb
 * bin/metrics-php-fpm.rb

## Usage

Make sure you adjust the `fastcgi_pass` socket to whatever you are using:

```
location ~ "/fpm-(status|ping)" {
  include       /etc/nginx/fastcgi_params;
  fastcgi_pass  unix:/var/run/php5-fpm.sock;
  fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
  access_log off;
  allow 127.0.0.1;
  deny all;
}
```

Alternatively, but keep in mind that "ifs are evil":

```
set $pool "php5-fpm";
if ($arg_pool) {
  set $pool $arg_pool;
}
location ~ "/fpm-(status|ping)" {
  include       /etc/nginx/fastcgi_params;
  fastcgi_pass  unix:/var/run/$pool.sock;
  fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
  access_log off;
  allow 127.0.0.1;
  deny all;
}
```

## Installation

[Installation and Setup](http://sensu-plugins.io/docs/installation_instructions.html)

## Notes
