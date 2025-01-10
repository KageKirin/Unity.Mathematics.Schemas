# ![Logo](Icon.png) Unity.Mathematics.Schemas

This repo consists of [FlatBuffer](https://flatbuffers.dev/) schemas
that are compiled for C#/.NET with [FlatSharp](https://github.com/jamescourtney/FlatSharp).

The main schema, `Unity.Mathematics.fbs` defines FlatBuffer structures that are directly compatible to
their eponymous C# structures defined by the Unity.Mathematics assembly.

The supplementary schema, `Unity.Mathematics.Tables.fbs` defines FlatBuffer tables containing single values of arrays
of the aforementationed structures that can be de/serialialized. This schema is mostly intended for usage by the unit tests,
and as an integration example.

## ⚡ tl;dr or _I just want to fetch the correct dependency_

### dotnet CLI

```bash
dotnet add package UnityMathematics.Schemas --version x.y.z
```

### `Directory.Packages.props`

```xml
  <ItemGroup>
    <PackageVersion Include="UnityMathematics.Schemas" Version="x.y.z" />
  </ItemGroup>
```

### Schema only (i.e. for integration and recompilation by local project)

```xml
  <ItemGroup Label="dependencies">
    <PackageReference Include="UnityMathematics.Schemas" GeneratePathProperty="true">
      <IncludeAssets>contentfiles</IncludeAssets>
      <PrivateAssets>all</PrivateAssets>
    </PackageReference>
  </ItemGroup>

  <ItemGroup Label="schemas">
    <!-- compile UnityMathematics.fbs -->
    <FlatSharpSchema Include="$(UnityMathematics_Schemas)\content\**\*.fbs">
      <IncludePath>$(UnityMathematics_Schemas)\content</IncludePath>
    </FlatSharpSchema>

    <!-- compile your own schemas -->
    <FlatSharpSchema Include="$(MSBuildThisFileDirectory)\**\*.fbs">
      <IncludePath>$(UnityMathematics_Schemas)\content</IncludePath>
    </FlatSharpSchema>
  </ItemGroup>
```

### Runtime only (i.e. for integration by local project, without recompilation)

```xml
  <ItemGroup Label="dependencies">
    <PackageReference Include="UnityMathematics.Schemas" />
  </ItemGroup>
```

### Schema and Runtime (i.e. for inclusion by local schema, without recompilation of the schema itself)

```xml
  <ItemGroup Label="dependencies">
    <PackageReference Include="UnityMathematics.Schemas" GeneratePathProperty="true">
      <IncludeAssets>all</IncludeAssets>
    </PackageReference>
  </ItemGroup>

  <ItemGroup Label="schemas">
    <!-- compile your own schemas -->
    <FlatSharpSchema Include="$(MSBuildThisFileDirectory)\**\*.fbs">
      <IncludePath>$(UnityMathematics_Schemas)\content</IncludePath>
    </FlatSharpSchema>
  </ItemGroup>

  <PropertyGroup Label="FlatSharp compiler configuration">
    <FlatSharpInputFilesOnly>true</FlatSharpInputFilesOnly>
  </PropertyGroup>
```

For further information, please refer to the
[FlatSharp compiler documentation](https://github.com/jamescourtney/FlatSharp/wiki/Compiler).

## 🔧 Schema usage

Define your types using the same namespace as you would in C#.

```fbs
include "Unity.Mathematics.fbs";

namespace Example;

struct Transform {
  position: Unity.Mathematics.float3;
  rotation: Unity.Mathematics.quaternion;
  scale: Unity.Mathematics.float3;
}

table Mesh {
  transform: Transform (required);
  vertices: [Unity.Mathematics.float3] (required);
  normals: [Unity.Mathematics.float3] (required);
  uvs: [Unity.Mathematics.float2] (required);
  indices: [short] (required);
  //...
}

table ParticleEffect {
  transform: Transform (required);
  vertices: [Unity.Mathematics.float3] (required);
}
```

## 🤝 Collaborate with My Project

PRs are welcome.  
Please refer to [COLLABORATION.md](./COLLABORATION.md) for more details.
