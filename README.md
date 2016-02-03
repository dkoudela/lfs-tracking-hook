# LFS Tracking Hook
## Motivation
To register a concrete file to be tracked by the LFS, the right commands have to be executed in the right order.

The following example is taken from https://git-lfs.github.com/:

``git lfs track "*.psd"``

``git add file.psd``

``git commit -m "Add design file"``

``git push origin master``

These four commands have to be executed everytime a new file is added to the LFS repository.
If forgotten or executed in a different order, the files will not be tracked by the LFS and will be part of the standard git repository.

## Purpose
Git hook for automatic LFS tracking of specified files before commit
