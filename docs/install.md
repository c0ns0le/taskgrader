# Installing the taskgrader

## Dependencies

On many distributions, the required dependencies are already installed.

On **Debian or Ubuntu**, the recommended dependencies are:

    apt-get install build-essential git python python3 sudo

Some additional dependencies are required to support all features and languages, on Debian or Ubuntu:

    apt-get install fp-compiler gcj-4.9 nodejs php5-cli

On **Fedora**, the recommended dependencies are:

    dnf install @development-tools glibc-static libstdc++-static

Some systems don't provide the `gcj` shortcut, in that case make a symlink to your version of `gcj`, such as:

    ln -s /usr/bin/gcj-4.9 /usr/bin/gcj

### Control groups (for contest environments)

In a contest environment, you may want control groups enabled in your kernel:

    apt-get install cgroup-tools

On some kernels, you might need to (re)activate the memory subsystem of control groups (on Debian, you can check whether the folder `/sys/fs/cgroup/memory` is present).

You can do this by using the `cgroup_enable=memory` kernel option. On many systems, you can do that by editing `/etc/default/grub` to add:

    GRUB_CMDLINE_LINUX="cgroup_enable=memory"

and then executing `update-grub` as root. Once enabled, set `CFG_CONTROLGROUPS` to `True` in `config.py` (after installation) to enable their usage within the taskgrader.

Some more information can be found in the [isolate man page](http://www.ucw.cz/moe/isolate.1.html).

### On Windows

You can use the taskgrader in a Windows environment thanks to [Cygwin](https://cygwin.com). Most features will work, except isolate, and some languages which are not supported under Cygwin.

Download and install Cygwin from [its website](https://cygwin.com/install.html). Install the following dependencies (you can reexecute Cygwin's setup.exe anytime to install more dependencies):
`git python python3 gcc gcc-g++`.

You can then follow the next steps normally.

### On Mac OS X

The taskgrader works on Mac OS X normally.

On Mac OS X, `python` is an alias for `python3` instead of `python2` as on many systems; so take care to execute the taskgrader and tools with the `python2` command.

## Installation

Execute `install.sh` in the taskgrader directory to install, as the user who will be running the taskgrader. It will help you install everything.

The installation of 'isolate' needs root access, and ability to have files owned by root with setuid on the current directory (doesn't work with remote folders such as NFS). If you cannot, you won't be able to use 'isolate', but the taskgrader will still work.

If needed, edit `config.py` to suit your needs; however default values will work for simple tests.

## Testing

After configuration, you can test that the taskgrader is configured properly and is behaving as expected by running `tests/test.py`. By default, it will run all tests and give you a summary. Full usage instructions are given by `test.py -h`.

If you didn't install dependencies for all languages, some tests will fail.

## Usage

Now that the taskgrader is installed, you can use it as described in the [Basic Usage](basicusage.md) section.

For convenience, you can add some taskgrader commands by adding the `path/` subfolder of this repository into your `PATH` environment variable. You can do so by adding to your shell profile file (for instance `~/.bashrc` if you use `bash`):

    export PATH="/your/copy/of/taskgrader/path/:$PATH"

It will allow a few commands to be used directly in your shell, such as `taskstarter` or `taskgrader`. Check the `path/` folder to see the full list of commands.
