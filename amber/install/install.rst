Instalacja
----------

Instalacje należy wykonywać jako użytkownik ``panda`` w katalogu domowym użytkownia ``panda``: ``/home/panda``. Należy pobrać i zainstalować *Amber* wraz z dodatkami według poniższego skryptu:

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

Aktualizację platformy *Amber* z dodatkami można wykonać za pomocą poniższego skryptu, jako użytkownik ``panda``:

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
