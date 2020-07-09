# WIAS Julia Package Registry

This is a registry for Julia packages being developed at WIAS. 


## Accessing packages from this registry

In order to add this registry to your Julia environment, enter the package manager mode and issue
````
pkg> registry add https://github.com/WIAS-BERLIN/WIASJuliaRegistry
````
After this it will be possible to add packages registered in this registry via the usual Julia package manager commands.


## Workflow for registration of a new package or a new version

This workflow is currently being developed.

### Without write access to this repository

Send an  email to  one of  the admins  containing the  git url  of the corresponding repository singnaling the advance of a new version.  The `Project.toml` file already should contain the new version number.

### With write access to this repository

Add the [LocalRegistry.jl](https://github.com/GunnarFarneback/LocalRegistry.jl) package to your environment
````
pkg>  add LocalRegistry
````


For a new package `X.jl` or a new version thereof, first obtain a clone, either by checking it out via its url, or by adding it to the environment, getting into develop mode and updating it:
````
pkg> add X
pkg> develop X
pkg> update X # not clear if really necessary
````

Then, you will be able to register a new version based on the updated version number in `Project.toml`:

````
julia> using X
julia> using LocalRegistry
julia> LocalRegistry.register(X,"WIASJuliaRegistry",push=true)
````
This assumes that the remote origin of the local clone in `.julia/registries/WIASJuliaRegistry' has been modified to `git@github.com:WIAS-BERLIN/WIASJuliaRegistry`.
The `push=true` can be omitted, in this case, `LocalRegistry.Register` results in a commit to the local copy which you can push later.

## See also
- [Pkg.jl/Managing Packages](https://julialang.github.io/Pkg.jl/stable/managing-packages/)
- [Pkg.jl/Registries](https://julialang.github.io/Pkg.jl/stable/registries/)
- [LocalRegistry.jl](https://github.com/GunnarFarneback/LocalRegistry.jl)
- [HolyLabRegistry](https://github.com/HolyLab/HolyLabRegistry)
- [Julia notes of Lutz Hendricks](https://lhendricks.org/julia_notes.pdf) - see Ch. 18 (with exception of 18.7.2)
- Ignore anything mentioning `Registrator.jl`. It has been [replaced](https://discourse.julialang.org/t/creating-a-custom-registry/28007/14?u=j-fu) by `LocalRegistry.jl`
