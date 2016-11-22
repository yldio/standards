# General rules

## Filename case

Use `lower-case-and-dashes.ext`.

HFS+ (default file system in OSX) has optional case sensitivity, and the windows subsystem on NTFS is not case sensitive, which means that working on these configurations can lead to accidents when renaming files in a git repository for instance.

Sticking to the `lower-case-and-dashes.ext` will prevent this.
