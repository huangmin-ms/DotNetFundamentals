1. Ref structs were introduced mainly for the benefit of the **Span<T>** and **ReadOnlySpan<T>** structs. 
2. Ensure structs can only ever reside on the **stack**.
3. Attempting to use a ref struct in such a way that it could reside on the heap generates a compile-time error.
    - Class field
    - Generic Type Argument or Array type
    - Boxing
    - Async function
    - ...
 4. Metadata Representation: Ref-like structs will be marked with **System.Runtime.CompilerServices.IsRefLikeAttribute** attribute.
     ```
     [IsRefLike]
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
