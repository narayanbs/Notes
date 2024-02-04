#### Viewing file in a particular commit

The Git Show command allows us to view files as they existed in a previous state.

Output a file’s contents from a previous version of a file

`git show <version>:<file>`

The version can be a commit ID, tag, or even a branch name. The file must be the path to a file. For example, the following would output a contents of a file named internal/example/module.go file from a tagged commit called “release-23”.

`git show release-23:internal/example/module.go`

for ex: `git show 1258d3aa71c20124758315a7340906501687fd3f:lua/narayan/lsp/handlers.lua`

#### Getting commit id so that so that we can pin the plugins.

go to `~/.local/share/nvim/site/pack/packer/start/<plugin-folder>`
`git rev-parse HEAD`
