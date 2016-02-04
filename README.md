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

Additionally, ``git add`` and ``git lfs track`` behave differently in case of adding/tracking a content of subdirectories.
``git lfs track`` command does not recursively search in subdirectories unless an explicit glob expression is used.

Example:

``git lfs track "*.psd"`` will add all ``"*.psd"`` in the current directory.

``git add "*.psd"`` will add all ``"*.psd"`` in the current directory and its subdirectories.

## Purpose
This git hook matches filenames of newly committed files against given RegExp definition.
If a filename is matched, the git hook ensures the file is tracked by the LFS.
Files already indexed by git repository are not considered.

Using the example above, it is necessary just execute the standard git commands:

``git add file.psd``

``git commit -m "Add design file"``

``git push origin master``

## Installation
1. Install LFS and initialize the LFS by ccommand ``git lfs install`` (once per machine)
2. Create a file ``.gitlftracking`` in the root directory of the git repository.
3. Add regular expressions matching filenames of files to be tracked, e.g.:

   ``JArchitectOut.*\.jdar``

   ``*\.jpeg``
   
   ``database.*\.mdb``

4. Commit the file ``.gitlftracking`` to the git repository.
5. Copy the file https://github.com/dkoudela/lfs-tracking-hook/blob/master/pre-commit to the directory ``.git/hooks/`` in the git repository.

---

> Note 1.: 
> If you already have a pre-commit hook in your git repository, you have to merge the scripts together.

---

> Note 2.:
> As a pre-commit hook cannot be submitted to the git repository, the installation procedure has to be executed in every cloned git repository.

---
