
# Ansible Role:  `pacman`

Ansible role to configure pacman.

[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/bodsch/ansible-pacman/CI)][ci]
[![GitHub issues](https://img.shields.io/github/issues/bodsch/ansible-pacman)][issues]
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/bodsch/ansible-pacman)][releases]

[ci]: https://github.com/bodsch/ansible-pacman/actions
[issues]: https://github.com/bodsch/ansible-pacman/issues?q=is%3Aopen+is%3Aissue
[releases]: https://github.com/bodsch/ansible-pacman/releases


## Contribution

Please read [Contribution](CONTRIBUTING.md)

## Development,  Branches (Git Tags)

The `master` Branch is my *Working Horse* includes the "latest, hot shit" and can be complete broken!

If you want to use something stable, please use a [Tagged Version](https://github.com/bodsch/ansible-pacman/tags)!

## Configuration

There are predefined values for [Arch Linux](vars/archlinux.yml) and [Artix Linux](vars/artixlinux.yml).

```yaml
pacman_config: {}

pacman_repositories: {}

pacman_mirrors: {}

pacman_custom_mirrors: []
```

### `pacman_config`

```yaml
pacman_config:
  root_dir: "/"
  db_path: /var/lib/pacman/
  cache_dir: /var/cache/pacman/pkg/
  log_file: /var/log/pacman.log
  gpg_dir: /etc/pacman.d/gnupg/
  hook_dir: /etc/pacman.d/hooks/
  hold_pkg: pacman glibc
  xfer_command: /usr/bin/curl -L -C - -f -o %o %u
  # XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u
  clean_method: KeepInstalled
  architecture: auto
  # Pacman won't upgrade packages listed in IgnorePkg and members of IgnoreGroup
  ignore_pkg: []
  ignore_group: []
  no_upgrade: []
  no_extract: []

  # Misc options
  use_syslog: true
  color: true
  no_progress_bar: true
  check_space: true
  verbose_pkg_lists: false
  parallel_downloads: 5
  # By default, pacman accepts packages signed by keys that its local keyring
  # trusts (see pacman-key and its man page), as well as unsigned packages.
  sig_level:
    - Required
    - DatabaseOptional
  local_file_sig_level:
    - Optional
  remote_file_sig_level:
    - Required
```

### `pacman_repositories`

```yaml
pacman_repositories:
  custom:
    enabled: false
    sig_level:
      - Optional
      - TrustAll
    server: file:///home/custompkgs

  core:
    enabled: true
    include: /etc/pacman.d/mirrorlist

  extra:
    enabled: true
    include: /etc/pacman.d/mirrorlist

  community-testing:
    enabled: false
    include: /etc/pacman.d/mirrorlist

  community:
    enabled: true
    include: /etc/pacman.d/mirrorlist
```

### `pacman_mirrors`

```yaml
pacman_mirrors:
  "Default mirrors":
    enabled: true
    servers:
      - https://geo.mirror.pkgbuild.com/$repo/os/$arch
      - https://mirror.rackspace.com/archlinux/$repo/os/$arch
      - https://mirror.leaseweb.net/archlinux/$repo/os/$arch

  "Europe - Germany":
    enabled: true
    servers:
      - https://mirror.netcologne.de/artix-linux/$repo/os/$arch
      - http://mirrors.redcorelinux.org/artixlinux/$repo/os/$arch
      - https://mirror.pascalpuffke.de/artix-linux/$repo/os/$arch
      - https://ftp.uni-bayreuth.de/linux/artix-linux/$repo/os/$arch
```

### `pacman_custom_mirrors`

```yaml
pacman_custom_mirrors:
  - file: /etc/pacman.d/mirrorlist-arch
    "ARCH MIRRORS":
      enabled: false
      servers:
        - http://mirror.i3d.net/pub/archlinux/$repo/os/$arch
```


---

## Author and License

- Bodo Schulz

## License

[Apache](LICENSE)

`FREE SOFTWARE, HELL YEAH!`
