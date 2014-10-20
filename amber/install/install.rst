Instalacja
----------

Instalacje należy wykonywać w katalogu domowym użytkownia ``panda``. Należy pobrać i zainstalować *Amber* wraz z dodatkami.
::

    mkdir -p ${HOME}/amber
    pushd ${HOME}/amber
        git clone https://github.com/project-capo/amber-cpp-drivers.git
        pushd ${HOME}/amber/amber-cpp-drivers
            make clean
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
