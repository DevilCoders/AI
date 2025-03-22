```cmake
YQL_PYTHON3_UDF(check_analytics_info)
# Specifies that this is a Python 3 UDF (User-Defined Function) for YQL (Yandex Query Language).
# The UDF is named `check_analytics_info`.

OWNER(
    ran1s
    g:alice
)
# Specifies the owners of the UDF. This is typically used for ownership and access control in a collaborative environment.
# - `ran1s`: An individual owner (likely a username).
# - `g:alice`: A group owner (likely a team or organization).

REGISTER_YQL_PYTHON_UDF(
    NAME CustomPython3
)
# Registers the UDF with YQL under the name `CustomPython3`.
# This allows the UDF to be used in YQL queries.

PEERDIR(
    alice/acceptance/modules/check_analytics_info/lib
    contrib/python/click
    statbox/nile
    yt/python/yt/wrapper
    yql/library/python
)
# Lists the dependencies of the UDF using the `PEERDIR` macro. These are other libraries or modules that this UDF depends on.
# - `alice/acceptance/modules/check_analytics_info/lib`: The local library containing the checker implementations.
# - `contrib/python/click`: The `click` library for command-line interface functionality.
# - `statbox/nile`: The `nile` library for working with YT (Yandex Table).
# - `yt/python/yt/wrapper`: The `yt.wrapper` library for YT operations.
# - `yql/library/python`: The YQL Python library for YQL integration.

PY_SRCS(
    __main__.py
)
# Lists the Python source files included in this UDF using the `PY_SRCS` macro.
# - `__main__.py`: The main script file that defines the UDF logic.

END()
# Marks the end of the UDF definition. This macro is used to close the scope of the UDF configuration.
```
