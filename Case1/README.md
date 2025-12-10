# Documenter + History search = </3

- Load REPL, press Ctrl-R, it is instant.
- Load Documenter
- Precc Ctrl-R, it is very slow
- julia commit 5ee08163167

```julia
using SnoopCompileCore

invalidations = @snoop_invalidations begin
    using Documenter
end

using SnoopCompile
trees = invalidation_trees(invalidations)

...
 inserting convert(::Type{String}, x::JSON.PtrString) @ JSON ~/.julia/packages/JSON/0oqO1/src/lazy.jl:426 invalidated:
index!(::Dict{String, Union{Nothing, Tuple{Base.PkgId, String}}}, ::Nothing, ::Any) (45 children)
                 35: signature Tuple{typeof(convert), Type{String}, Any} triggered MethodInstance for setindex!(::Vector{String}, ::Any, ::Int64) (141 children)
                 36: signature Tuple{typeof(convert), Type{String}, Any} triggered MethodInstance for push!(::Vector{String}, ::Any) (163 children)
...

 inserting convert(::Type{Symbol}, x::JSON.PtrString) @ JSON ~/.julia/packages/JSON/0oqO1/src/lazy.jl:435 invalidated:
 ...
                 15: signature Tuple{typeof(convert), Type{Symbol}, Any} triggered MethodInstance for Base.ImmutableDict{Symbol, Any}(::Base.ImmutableDict{Symbol, Any}, ::Any, ::Any) (233 children)
                 16: signature Tuple{typeof(convert), Type{Symbol}, Any} triggered MethodInstance for setindex!(::Dict{Symbol, Bool}, ::Any, ::Any) (650 children)
                 17: signature Tuple{typeof(convert), Type{Symbol}, Any} triggered MethodInstance for @NamedTuple{region::UnitRange{Int64}, label::Symbol, value}(::NamedTuple{(:region, :label, :value)}) (763 children)
```
