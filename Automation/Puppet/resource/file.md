Remove directory

```puppet
file { '/etc/skel/.mozilla':
  ensure    => 'absent',
  recurse   => true,
  purge     => true,
  force     => true,
}
```

Remove all files and folders in directory

```puppet
file { '/etc/skel/.mozilla':
  ensure    => 'directory',
  recurse   => true,
  purge     => true,
  force     => true,
}
```