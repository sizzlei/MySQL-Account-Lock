# MySQL-Account-Lock


### Verion : MySQL / Percona 5.7 이상

@ Plugin Load
<code><pre>
INSTALL PLUGIN CONNECTION_CONTROL SONAME 'connection_control.so';
INSTALL PLUGIN CONNECTION_CONTROL_FAILED_LOGIN_ATTEMPTS SONAME 'connection_control.so'
</pre></code>

@ CNF ADD
<code><pre>
[mysqld]
plugin-load-add=connection_control.so
connection-control = FORCE_PLUS_PERMANENT
connection-control-failed-login-attempts = FORCE_PLUS_PERMANENT
</pre></code>

@ Unlock Account
<code><pre>
alter user 'user'@'host' account unlock;
</pre></code>
