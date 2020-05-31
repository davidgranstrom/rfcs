- Title: Include scnvim
- Date proposed: 2020-05-30
- RFC PR: https://github.com/supercollider/rfcs/pull/0000 **update this number after RFC PR has been filed**

# Summary

[scnvim](https://github.com/davidgranstrom/scnvim) is a SuperCollider frontend for [Neovim](https://github.com/neovim/neovim). This RFC was created to discuss whether or not scnvim should be included as an official SuperCollider editor frontend.

# Motivation

* Add another editor frontend to interface with SuperCollider.

# Specification

scnvim would be added as submodule in the main repository with the other editor frontends (sc-ide, scvim, scel, sced).

The following steps would be needed:

- Transfer the scnvim repository to the SuperCollider repository.
  - Preserving commit history, issues and PRs would be ideal.

- Make additions to the build system
  - Add `CMakeLists.txt` rules in the scnvim root.
  - Add build option for scnvim in `editors/CMakeLists.txt`

- Update `SCClassLibrary/DefaultLibrary/Main.sc:startup` to include a note about scnvim

- Update the *Editor* section on the [community page](https://supercollider.github.io/community/systems-interfacing-with-sc).

# Differences from scvim

I have not kept a list of differences to scvim, but here are a few:

* `sclang` process is started and owned by `nvim`.
* Post window output is displayed in a native vim buffer.
* Alternative approach to mappings (uses `<Plug>` mappings instead of autocmds).
* Can be "lazy loaded" - most of the plugin is implemeted in `autoload/`.
* Ability to render scdoc helpfiles in vim buffers
  - Requires `pandoc` at the moment, but a native parser could be added in lua in the future.
* Supports `thisProcess.nowExecutingPath`, `.loadRelative` etc. that needs to know the current path.
* No external interpreters needed (i.e. `ruby`)

# Drawbacks

* Users of scnvim will have to update their nvim configuration to point to the official fork at `supercollider/scnvim` to get the latest updates.

* Because of a misunderstanding on my part about editor specific extension (`scide_*`), I erroneously used `scide_scvim` for the SCNvim*.sc classes. Changing this now will cause a conflict for existing users of scnvim, but will be better to get correct in the long term (e.g. if scvim implements its own `Document` class).

# Unresolved Questions

A very common user issue has been about the installation of the SCNvim SuperCollider classes. I have created two solution for this [PR 72](https://github.com/davidgranstrom/scnvim/pull/72) and [PR 86](https://github.com/davidgranstrom/scnvim/pull/86). Ideally one of them should be merged before a potential inclusion of the plugin to the SuperCollider repo. (I'm leaning towards #86).
