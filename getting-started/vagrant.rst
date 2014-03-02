.. highlight:: bash

========================================
Vagrant (Virtualization, not emulation!)
========================================

playdoh comes with out-of-the-box support for running your web app in a
`virtual machine <http://en.wikipedia.org/wiki/Virtual_machine>`_. Basically,
this means that you can easily get started developing a playdoh app on your
local machine without having to futz with virtualenvs, dependencies, compiling
things, or lots of other annoying things that make it a pain to hit the ground
running when you start a new app.

How Does it Work?
-----------------

playdoh uses `VirtualBox <https://www.virtualbox.org/>`_, `Vagrant
<http://vagrantup.com/>`_, and `puppet <http://puppetlabs.com/>`_ to do its
magic. Vagrant allows for us to easily customize and access our virtual
machines; puppet lets us run custom commands (like installing MySQL or
setting up databases); and VirtualBox runs our created VMs.

The virtual machine mounts your app's directory inside its home directory so
the changes you make on your host machine are reflected instantly inside your
VM without any weird FTPing or other such barbaric nonsense.

It just works!

How Do I Get Started?
---------------------
You'll need VirtualBox and vagrant to get started. Head over to the `VirtualBox
downloads page <https://www.virtualbox.org/wiki/Downloads>`_ and get the
latest version of VirtualBox for your host operating system (if you run Mac OS
X, select the Mac version). Don't worry about guest operating system; vagrant
take care of that for you.

Next, install vagrant. Go to the `Vagrant downloads page <http://downloads.vagrantup.com/>`_ 
and get the latest version of vagrant for your operating system.

**That's it!** You're ready to boot the playdoh VM and access your webapp from
inside it.

How Do I Boot and Access My VM?
-------------------------------

If you don't yet have a project directory, you'll want to recursively clone the
playdoh repository::

    git clone https://github.com/mozilla/playdoh.git my_project_directory --recursive

Then, enter the directory and tell vagrant to spin up a VM::

    cd ~/my_project_directory
    vagrant up

Done! That's all it takes for your VM to be created and boot! If you're running
this for the first time, it will take awhile for your base VM image to download
and for puppet to install all the necessary packages, so it might be wise to
get a coffee or `watch a YouTube video
<http://www.youtube.com/watch?v=LJ1TIYxm1vM>`_.

Once your VM is booted, just run ``vagrant ssh`` to ssh into your VM. ``cd``
into your projects directly and run whatever manage.py commands you like.

playdoh's vagrant setup takes the liberally of forwarding port 8000 (the usual
Django development port), so if you want to access your web app, do the
following (after using ``vagrant ssh`` to get into your VM)::

    cd project
    ./manage.py runserver 0.0.0.0:8000

Note that you'll need to explicitly set the host and port for runserver to
be accessible from outside the VM.

Learn more about Vagrant by `checking out its docs
<http://docs.vagrantup.com/v2/getting-started/index.html>`_ and enjoy not caring
about which libraries are installed on your system anymore!
