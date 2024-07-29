##### Create .clang-format file at the source root
$ clang-format -style=llvm -dump-config > .clang-format

##### Modify the following lines in .clang-format
ColumnLimit: 100
MaxEmptyLinesToKeep: 1
SeparateDefinitionBlocks: Always

##### Create a .gitignore file and add the following
```
.vscode

build/*
*.pbxuser
*.mode2v3
*.mode1v3
*.perspective
*.perspectivev3
*~.nib

#ignore private workspace stuff added by Xcode4
xcuserdata
project.xcworkspace

## generic files to ignore
*~
*.lock
*.DS_Store
*.swp
*.out

# Compiled Object files
*.slo
*.lo
*.o
*.obj

# Compiled Dynamic libraries
*.so
*.dylib
*.dll

# Fortran module files
*.mod

# Compiled Static libraries
*.lai
*.la
*.a
*.lib

# Executables
*.exe
*.out
*.app
```
