# Integrating with C++

## The C++

In order to demonstrate the connection between C++ and QML in Qt for MCUs, we will create a simple ``Counter`` singleton holding an integer value. It provides a property, ``value``, as well as methods for changing the value, ``increase`` and ``decrease``, as well as a ``reset`` method. It also provides a signal, ``hasBeenReset``. All of this is provided from the ``Counter`` class shown below

::: warning TODO
Counter class
:::

Coming from Qt, this looks odd. This is where Qt for MCUs shows the main differences. There is no ``QObject`` base class or ``Q_OBJECT`` macro, instead a new set of classes from the ``Qul`` is used. In this particular case, the base class is the ``Qul::Singleton`` class, creating a globally accessible singleton in the QML world. We also use the ``Qul::Signal`` class to create a signal and the ``Qul::Property`` class to create a property. All public, non-overloaded member functions are exposed to QML automatically.

::: tip
To create a class that can be instatiated from QML, instead of a singleton, use the ``Qul::Object`` base class.
:::

The class is then exposed to QML using the CMake macro ``qul_target_generate_interfaces``. Below you can see the ``CMakeLists.txt``, based on the file generated by Qt Creator, with the ``counter.h`` and ``counter.cpp`` files added.

Now, let's continue with the implementation of the ``Counter`` class. First up, for the ``value`` property, we use the ``value`` and ``setValue`` functions to access and modify the actual value. In our case, the property holds and ``int``, but just as for the ordinary QML engine, types are [mapped between C++ and QML](https://doc.qt.io/QtForMCUs/qtul-integratecppqml.html#type-mapping).

::: warning TODO
code for the property, including the + and - functions
:::

The signal is represented by the ``Qul::Signal`` instance named ``hasReset``. The signal takes a function signature as template argument, so to create a signal carrying an integer, create a ``Qul::Signal<void(int)>``. In this case, the signal does not carry any values, so it is defined as a `void(void)`. To emit the signal, we simply call it as if it was an ordiary function as shown in the ``reset`` function below.

::: warning TODO
the signal
:::

## The QML

::: warning TODO
screenshot
integration of Counter
    buttons for functions
    flash on reset
    show value
:::



::: tip Links
Further reading at qt.io:
* [Integrate C++ and QML](* https://doc.qt.io/QtForMCUs/qtul-integratecppqml.html)
:::