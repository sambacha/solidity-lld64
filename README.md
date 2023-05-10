# solc-lld64


50086 solc-lld64

52371 solc-std


Version: 0.8.21-develop.2023.5.10+commit.f07c8b1f.Darwin.appleclang
Version: 0.8.20-ci.2023.5.10+commit.a1b79de6.mod.Darwin.appleclang

```bash 
TZ=UTC git show --quiet --date="format-local:%Y.%-m.%-d" --format="ci.%cd" >prerelease.txt
cmake .. -DUSE_Z3=OFF -DUSE_CVC4=OFF -DSOLC_LINK_STATIC=ON -DSOLC_STATIC_STDLIBS=ON -DCMAKE_OSX_ARCHITECTURES='arm64' --fresh
```

```diff
# File: EthCompilerSettings.cmake
#
#! Note:  -fuse-ld=lld --ld-path=$HOME/ld64.lld
#


 if (("${CMAKE_CXX_COMPILER_ID}" MATCHES "GNU") OR ("${CMAKE_CXX_COMPILER_ID}" MATCHES "Clang"))
    	option(USE_LD_GOLD "Use GNU gold linker" ON)
	 if (USE_LD_GOLD)
+	 	execute_process(COMMAND ${CMAKE_CXX_COMPILER} -fuse-ld=lld --ld-path=$HOME/ld64.lld -Wl,--version ERROR_QUIET OUTPUT_VARIABLE LD_VERSION)
		if ("${LD_VERSION}" MATCHES "GNU gold")
+			set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fuse-ld=lld --ld-path=$HOME/ld64.lld")
		endif ()
	endif ()
endif ()
```
