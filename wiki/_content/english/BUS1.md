BUS1 is a work-in-progress in-kernel IPC mechanism.

## Trying it out

**Warning:** BUS1 is in heavy development, and should not be considered ready to use

Install [libbus1-git](https://aur.archlinux.org/packages/libbus1-git/), then load the module:

```
# modprobe bus1

```

Now you should see `/dev/bus1` virtual device in your system.

## See also

*   [BUS1 homepage](http://www.bus1.org/)