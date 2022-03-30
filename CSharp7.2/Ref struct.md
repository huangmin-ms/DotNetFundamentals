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
 5. User Sceanrios:
    1. Optimize code and reduce load on GC.
    2. Encapsulates other ref structs
        ```
        ref struct SampleRefStruct
        {
            Span<int> intSpan;
            Span<double> doubleSpan;
        }
        ```
 6. Commonly used ref structs in .NET platform
    - [Span<T>](https://github.com/dotnet/runtime/blob/main/src/libraries/System.Private.CoreLib/src/System/Span.cs)
    - [ReadOnlySpan<T>](https://github.com/dotnet/runtime/blob/main/src/libraries/System.Private.CoreLib/src/System/ReadOnlySpan.cs)
    - [Utf8JsonReader](https://github.com/dotnet/runtime/blob/main/src/libraries/System.Text.Json/src/System/Text/Json/Reader/Utf8JsonReader.cs)
    
  References:
  1. [C# 8.0 in a Nutshell](https://learning.oreilly.com/library/view/c-8-0-in/9781492051121/ch03.html#ref_structs)
  2. [ref structs in C# 7.2](https://kalapos.net/Blog/ShowPost/DotNetConceptOfTheWeek16-RefStruct)
    
