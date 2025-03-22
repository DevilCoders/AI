```cmake
# Defines a Python 3 executable program using Yandex's build system
PY3_PROGRAM()  

# Specifies the owner(s) of this program
OWNER(  
    ran1s  # Individual owner of the program
    g:alice  # Group owner (group: alice)
)

# Declares dependencies on other modules and libraries required for the program
PEERDIR(  
    contrib/python/click  # Dependency on Click, a Python CLI framework

    alice/acceptance/modules/check_analytics_info/lib  # Dependency on the analytics checkers library
)

# Specifies the Python source file that serves as the main entry point for execution
PY_SRCS(  
    __main__.py  # The main script that will be executed when running the program
)

# Marks the end of the `ya.make` configuration
END()
```
