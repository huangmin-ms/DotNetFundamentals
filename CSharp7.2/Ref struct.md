1. Ref structs were introduced mainly for the benefit of the **Span<T>** and **ReadOnlySpan<T>** structs. 
2. Ensure structs can only ever reside on the **stack**.
3. Attempting to use a ref struct in such a way that it could reside on the heap generates a compile-time error.
    - Class field
    - Generic Type Argument or Array type
    - Boxing
    - Async function
    - ...
 4. Metadata Representation: Ref-like structs will be marked with **System.Runtime.CompilerServices.IsByRefLikeAttribute** attribute.
     ```
     [IsByRefLike]
     ref struct MyStruct 
     {

     } 
     ```
 5. Disposable ref struct in C# 8.0  
    In C# 7.2, ref structs are not allowed to implement IDisposable. 
    But in C# 8.0 we can make them disposable by simply defining the Dispose method.
    ```
     ref struct MyStruct 
     {
           public void Dispose()  
           {  

           }  
     } 
    ```
    Example:[ValueUtf8Converter](https://github.com/dotnet/corefx/blob/a10890f4ffe0fadf090c922578ba0e606ebdd16c/src/Common/src/System/Text/ValueUtf8Converter.cs)
 6. User Sceanrios:
    1. Optimize code and reduce load on GC.
    2. Encapsulates other ref structs
        ```
        ref struct SampleRefStruct
        {
            Span<int> intSpan;
            Span<double> doubleSpan;
        }
        ```
 7. Commonly used ref structs in .NET platform
    - [Span<T>](https://github.com/dotnet/runtime/blob/main/src/libraries/System.Private.CoreLib/src/System/Span.cs)
    - [ReadOnlySpan<T>](https://github.com/dotnet/runtime/blob/main/src/libraries/System.Private.CoreLib/src/System/ReadOnlySpan.cs)
    - [Utf8JsonReader](https://github.com/dotnet/runtime/blob/main/src/libraries/System.Text.Json/src/System/Text/Json/Reader/Utf8JsonReader.cs)
    
  References:
  1. [C# 8.0 in a Nutshell](https://learning.oreilly.com/library/view/c-8-0-in/9781492051121/ch03.html#ref_structs)
  2. [ref structs in C# 7.2](https://kalapos.net/Blog/ShowPost/DotNetConceptOfTheWeek16-RefStruct)
    
