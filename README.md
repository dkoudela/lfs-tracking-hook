# LFS Tracking Hook
## Motivation
To register a concrete file to be tracked by the LFS, the right commands have to be executed in the right order.

The following example is taken from https://git-lfs.github.com/:

``git lfs track "*.psd"``

``git add file.psd``

``git commit -m "Add design file"``

``git push origin master``

These four commands have to be executed every time a new file is added to the LFS repository.
If forgotten or executed in a different order, the files will not be tracked by the LFS and will be part of the standard git repository.

## Purpose
This git hook matches filenames of newly committed files against given RegExp definition.
If a filename is matched, the git hook ensures the file is tracked by the LFS.
Files already indexed by git repository are not considered.

## Installation
1. Create a file ``.gitlftracking`` in the root directory of the git repository.
2. Add regular expressions matching filenames of files to be tracked, e.g.:

   ``JArchitectOut.*\.jdar``

   ``*\.jpeg``
   
   ``database.*\.mdb``

3. Commit the file ``.gitlftracking`` to the git repository.
4. Copy the file https://github.com/dkoudela/lfs-tracking-hook/blob/master/pre-commit to the directory ``.git/hooks/`` in the git repository.
