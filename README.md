# Automatic Native (Unmanaged) Library Importing for C#

It can be very difficult to distribute a C# assembly which relies on an unmanaged shared library to work in a cross platform environment.  Although ```[DllImport]``` is cross platform, it does not automatically deal with differences between 32 and 64 bit processes, and attempts to get it to do so are problematic.  It also does not allow unloading of a loaded library.

This is a simple ``.cs`` file that you can include in your project.

Instead of defining ```[DllImport]``` attributes above methods, you create one abstract class per unmanaged library and then call Auto.Import<MyClass>("mylib") to get an instance of a class derived from your abstract class and linked to the unmanaged library.

## Example usage
```
class Native {
	public static Native Instance = Auto.Import<Native>("mylibrary");

	public abstract void ExternalFunc(int arg1);
}
```

## Structure

You should put your unmanaged libraries into a structure like this:

```
native/i386/mylibrary.dll
native/i386/mylibrary.dylib
native/i386/mylibrary.so
native/amd64/mylibrary.dll
native/amd64/mylibrary.dylib
native/amd64/mylibrary.so
```

Include them in your project as content and copy if newer.