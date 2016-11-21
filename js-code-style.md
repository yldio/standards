# Javascript Code Style

## eslint with the `eslint-config-airbnb-base` preset, `eslint-config-airbnb` for React projects;

We can start a project to extend one of those bases if we find we have issues with some rules.

## Webpack and Babel

Rollup and Bublé might be tempting but we don't have any production experience with them, as soon as someone starts getting some at home experience we can start doing safer things with this on clients and then bigger things.

## Filename case

Use `lower-case-and-dashes.ext`.

HFS+ (default file system in OSX) has optional case sensitivity, and the windows subsystem on NTFS is not case sensitive, which means that working on these configurations can lead to accidents when renaming files in a git repository for instance.

Sticking to the `lower-case-and-dashes.ext` will prevent this.
