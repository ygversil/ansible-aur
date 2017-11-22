*ansible-aur* is an ansible module to use some aur helpers.

Currently, we support the following AUR helpers:

- pacaur (recommended, default)
- yaourt

## Usage

1. Add as a submodule in your playbook:

   ```
   mkdir -p library/external_modules
   git submodule add git://github.com/cdown/ansible-aur.git library/external_modules/ansible-aur
   ```


2. Link the binary to the base of `library/`:

   ```
   ln -s external_modules/ansible-aur/aur library/aur
   ```

3. Use it in a task, as in the following examples:

   ```
   # Install (using pacaur)
   - aur: name=yturl
     become:yes
     become_user: some_user_that_has_nopasswd_in_sudoers_for_pacman_u

   # Install (using yaourt)
   - aur: name=yturl tool=yaourt
     [...]

   # Remove (can also be done with the pacman resource)
   - aur: name=yturl state=absent
     [...]

   # Remove with dependencies
   - aur: name=yturl state=absent cascade=true
     [...]

   # Remove recursively (can also be done with the pacman resource)
   - aur: name=yturl state=absent recurse=true
     [...]
   ```
