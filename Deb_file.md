# Unpack, modify and repack deb files


There are instances when you need to modify some file(s) inside a deb package and repack it for installation.

This can be done very easily on _Ubuntu_ and _Debian_ using `dkpg-deb`

-----

1. Copy the `deb` file into a directory

2. Create the directory structure
   ```bash
   $ mkdir -p newpack oldpack/DEBIAN
   ```
    
3. Extract the filesystem tree
   ```bash
   $ dpkg-deb -x file.deb oldpack/
   ```
    
4. Extract the control information files
   ```bash
   $ dpkg-deb -e file.deb oldpack/DEBIAN
   ```

5. Modify what that you need

6. Repackage the deb file under newpack directory using `xz` compression
   ```bash
   $ dpkg-deb -Z xz -b oldpack/ newpack/
   ```
