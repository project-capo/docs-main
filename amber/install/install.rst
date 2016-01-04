Installation
------------

Installation need to be done as ``panda`` user in home directory of this user: ``/home/panda``. Need to download and install *Amber* with extras with following script:

.. code-block:: sh

    mkdir -p ${HOME}/amber
    pushd ${HOME}/amber
        git clone https://github.com/project-capo/amber-cpp-drivers.git
        pushd ${HOME}/amber/amber-cpp-drivers
            make all
        popd
        git clone https://github.com/project-capo/amber-python-drivers.git
        pushd ${HOME}/amber/amber-python-drivers
            ${HOME}/amber/amber-python-drivers/bin/install.sh
        popd
        git clone https://github.com/project-capo/amber-erlang-mediator.git
        pushd ${HOME}/amber/amber-erlang-mediator
            make all
        popd
    popd

Update of *Amber* platform with extras can be done with following script executed as ``panda``:

.. code-block:: sh

    pushd ${HOME}/amber/amber-cpp-drivers
        make clean
        git pull
        make all
    popd
    pushd ${HOME}/amber/amber-python-drivers
        ${HOME}/amber/amber-python-drivers/bin/uninstall.sh
        git pull
        ${HOME}/amber/amber-python-drivers/bin/install.sh
    popd
    pushd ${HOME}/amber/amber-erlang-mediator
        make clean
        make allclean
        git pull
        make all
    popd
