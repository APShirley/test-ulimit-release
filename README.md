Demos an issue introduced in `ubuntu-xenial` and not affecting `ubuntu-trusty` bosh stemcells regarding ulimits failing to be passed through when forking a process using `su` and how to fix it.

The issue is due to a change in xenial to `/etc/pam.d/su` which can be seen in [this changelog](http://changelogs.ubuntu.com/changelogs/pool/main/s/shadow/shadow_4.2-3.1ubuntu5.3/changelog):
```
  * debian/login.su.pam: Enable pam_limits by default. Closes: #705301
```

Each branch shows a different version of the bosh release: deploy on `trusty` to see original behavior, deploy on `xenial-broken` to see the breaking change or deploy on `xenial-fixed` to see the fix working. You can see how the limits change on the vm: `less /var/vcap/sys/log/test-ulimit/combined.log`

Further reading on why `su` is not how you should drop privileges http://jdebp.eu./FGA/dont-abuse-su-for-dropping-privileges.html
