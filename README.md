# Ansible Collection - kewlfft.aur

## Description
This collection includes an Ansible module to manage packages from the AUR.

### Installation
To install this collection from Ansible Galaxy run the following command:
``` shell
$ ansible-galaxy collection install kewlfft.aur
```

Alternatively, you can include the collection in a `requirements.yml` file and then run `ansible-galaxy collection install -r requirements.yml`. Here is an example `requirements.yml` file:
``` yaml
collections:
  - name: kewlfft.aur
```

## kewlfft.aur.aur Module
Ansible module to use some Arch User Repository (AUR) helpers as well as makepkg.

The following helpers are supported and automatically selected, if present, in the order listed below:
- [yay](https://github.com/Jguer/yay)
- [paru](https://github.com/Morganamilo/paru)
- [pacaur](https://github.com/E5ten/pacaur)
- [trizen](https://github.com/trizen/trizen)
- [pikaur](https://github.com/actionless/pikaur)
- [aurman](https://github.com/polygamma/aurman) (discontinued)

*makepkg* will be used if no helper was found or if it is explicitly specified:
- [makepkg](https://wiki.archlinux.org/index.php/makepkg)

### Options
|Parameter      |Choices/**Default**                                          |Comments|
|---            |---                                                          |---|
|name           |                                                             |Name or list of names of the package(s) to install or upgrade.|
|state          |**present**, latest                                          |Desired state of the package, 'present' skips operations if the package is already installed.|
|upgrade        |yes, **no**                                                  |Whether or not to upgrade whole system.|
|use            |**auto**, yay, paru, pacaur, trizen, pikaur, aurman, makepkg |The tool to use, 'auto' uses the first known helper found and makepkg as a fallback.|
|extra_args     |**null**                                                     |A list of additional arguments to pass directly to the tool. Cannot be used in 'auto' mode.|
|aur_only       |yes, **no**                                                  |Limit helper operation to the AUR.|
|local_pkgbuild |Local directory with PKGBUILD, **null**                      |Only valid with makepkg or pikaur. Don't download the package from AUR. Build the package using a local PKGBUILD and the other build files.|
|skip_pgp_check |yes, **no**                                                  |Only valid with makepkg. Skip PGP signatures verification of source file, useful when installing packages without GnuPG properly configured.|
|ignore_arch    |yes, **no**                                                  |Only valid with makepkg. Ignore a missing or incomplete arch field, useful when the PKGBUILD does not have the arch=('yourarch') field.|

#### Note
* Either *name* or *upgrade* is required, both cannot be used together.
* In the *use*=*auto* mode, makepkg is used as a fallback if no known helper is found.

### Usage
To use this module in a playbook or a role you have two options:
1. Refer to the module using it's FQCN (Fully Qualified Collection Name) `kewlfft.aur.aur`. This is the preferred method.
2. If you'd like to refer to the module using its unqualifed name `aur`, you can use the `collections` keyword to instruct Ansible to search for the module in the `kewlfft.aur` collection. Please see Ansible's [Using Collections](https://docs.ansible.com/ansible/latest/user_guide/collections_using.html#simplifying-module-names-with-the-collections-keyword) documentation for more information.

#### Notes
* The scope of this module is installation and update from the AUR; for package removal or for updates from the repositories, it is recommended to use the official *pacman* module.
* The *--needed* parameter of the helper is systematically used, it means if a package is up-to-date, it is not built and reinstalled.

#### Create the "aur_builder" user
While Ansible expects to SSH as root, makepkg or AUR helpers do not allow executing operations as root, they fail with "you cannot perform this operation as root". It is therefore recommended to create a user, which is non-root but has no need for password with pacman in sudoers, let's call it *aur_builder*.

This user can be created in an Ansible task with the following actions:
```
- name: Create the `aur_builder` user
  ansible.builtin.user:
    name: aur_builder
    create_home: no
    group: wheel

- name: Allow the `aur_builder` user to run `sudo pacman` without a password
  ansible.builtin.lineinfile:
    path: /etc/sudoers.d/11-install-aur_builder
    line: 'aur_builder ALL=(ALL) NOPASSWD: /usr/bin/pacman'
    create: yes
    validate: 'visudo -cf %s'
```

#### Examples
Use it in a task, as in the following examples:
``` yaml
- name: Install trizen using makepkg if it isn't installed already
  kewlfft.aur.aur:
    name: trizen
    use: makepkg
    state: present
  become: yes
  become_user: aur_builder

- name: Install package_name using the first known helper found
  kewlfft.aur.aur:
    name: package_name
  become: yes
  become_user: aur_builder

- name: Install package_name_1 and package_name_2 using yay
  kewlfft.aur.aur:
    use: yay
    name:
      - package_name_1
      - package_name_2

# Note: Dependency resolution will still include repository packages.
- name: Upgrade the system using yay, only act on AUR packages.
  kewlfft.aur.aur:
    upgrade: yes
    use: yay
    aur_only: yes

# Skip if it is already installed
- name: Install gnome-shell-extension-caffeine-git using pikaur and a local PKGBUILD.
  kewlfft.aur.aur:
    name: gnome-shell-extension-caffeine-git
    use: pikaur
    local_pkgbuild: {{ role_path }}/files/gnome-shell-extension-caffeine-git
    state: present
  become: yes
  become_user: aur_builder
```
