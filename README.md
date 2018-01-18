# The title of your library here, either `indirection.inc` or `My Cool Library`

[![sampctl](https://shields.southcla.ws/badge/sampctl-indirection-2f2f2f.svg?style=for-the-badge)](https://github.com/Y-Less/indirection)

Indirection is a system for calling function pointers in a generic and type-safe way.  Instead of `CallLocalFunction`, `Call`, `defer`, `Callback_Call`, or any other method, this gives one common interface which can be extended by library authors; utilising tags for compile-time parameters:

```pawn
ExampleFunction(Func:a<iisi>, playerid)
{
	@.a(playerid, _:a, "Hello World", random(5));
}
```

## Installation

Simply install to your project:

```bash
sampctl package install Y-Less/indirection
```

Include in your code and begin using the library:

```pawn
#include &lt;indirection>
```

## Usage

### General Users

To call a function that expects a function pointer, you can use `addressof` (from amx_assembly):

```pawn


FuncWithCallback(addressof (MyPublic));


### Library Writers

A parameter that takes a function pointer has the tag `Func:`, and is followed by the type specifier for the function.  For example `OnPlayerCommandText` would be `Func:func<is>` and `OnUnoccupiedVehicleUpdate` would be `Func:func<iiiffffff>`.  In a function signature this would look like:

```pawn
MyFunction(playerid, Func:func<ifis>)
{
}
```

Pointers are regular variables, so can be stored and copied as normal.  If you are going to use the pointer (i.e. call the function at some point in the future), you must call `Func_Claim` first - some pointers may have additional details associated with them, and this data must be retained.  Once you are done with the pointer (i.e. have called it all the times you want), call `Func_Release` on it.  For those of you familiar with *y_inline*, this is similar to `Callback_Get` and `Callback_Free` (but more generic).  While `Func_Claim` is not restricted by needing to be called in the first function, it must be called before the first function ends.

### MySQL Example:

x


### Low-Level Providers




> Write your code documentation or examples here. If your library is documented in the source code, direct users there. If not, list your API and describe it well in this section. If your library is passive and has no API, simply omit this section.



## Testing

To test, simply run the package:

```bash
sampctl package run
```

And connect to `localhost:7777` to test.
