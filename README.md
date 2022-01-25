# desktop-lfs
A tutorial how to install desktop (MATE in this case) on Linux from scratch

### What do you need

You will need LFS 10.1 or higher, wget, gcc and make.

### Starting

Log in as root, make sure that you have at least 5gb of free disk space,

download and unpack the current pkgsrc branch with:

    wget http://cdn.netbsd.org/pub/pkgsrc/current/pkgsrc.tar.xz -O /root/pkgsrc.tar.xz
    tar xJvf /root/pkgsrc.tar.xz -C /usr/


Next, bootstrap pkgsrc to /opt/pkg:

    cd /usr/pkgsrc/bootstrap
    ./bootstrap --prefix /opt/pkg --prefer-pkgsrc yes --make-jobs $(nproc)


After that, export the path:

    export PATH=/opt/pkg/sbin:/opt/pkg/bin:$PATH
    echo "!!" >> ~/.bashrc


Next, build a problematic package called glib2:

    cd /usr/pkgsrc/devel/glib2
    bmake install

It may take up to two hours.

Next, build xorg:

    cd /usr/pkgsrc/meta-pkgs/modular-xorg
    bmake install

It will take up to 8 hours, due to building llvm

And the final (or not yet) step - build MATE:

    cd /usr/pkgsrc/meta-pkgs/mate
    bmake install

Then add 'exec mate-session' to your .xinitrc and use startx to start the desktop
