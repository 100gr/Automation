A file/dir exists conditional

```puppet
exec {"check_presence":
  command => '/bin/true',
  onlyif => '/usr/bin/test -e /path/must/be/available',
}

whatever {"foo...":
  .....
  require => Exec["check_presence"],
}
```