Glide is an open source package manager for the Go programming language. It's written in Go.
Offered featues:

  * Package initialization, scans the existing project transitive dependnencies and adds them to a glide.yaml file
  * Installing and updating dependencies from existing files
  * Adding and removing dependencies
  * Records dependency information in a glide.yaml file. This includes a name, version or version range, version control information for private repos or when the type cannot be detected, and more.
  * Tracks the specific revision each package is locked to in a glide.lock file. This enables reproducibly fetching the dependency tree.
  * Works with Semantic Versions and Semantic Version ranges.
  * Supports Git, Bzr, HG, and SVN. These are the same version control systems supported by go get.
  * Utilizes vendor/ directories, known as the Vendor Experiment, so that different projects can have differing versions of the same dependencies.
  * Allows for aliasing packages which is useful for working with forks.
  
The tool is designed to work with go paths, thus it saves the packages in the $GOPATH or vendor/ directory in the project. The advanced features, such as current depedency detection will not work for us as it is Go specific, however it will be quite straight forward to modify the code base to save the packages at a custom location. 
We can reuse the majority of the code that is associated with retrieving packages from version control, installing, removing and maintaining packages.


A sample glide.yaml looks as follows:

```yaml
package: github.com/Masterminds/glide
homepage: https://masterminds.github.io/glide
license: MIT
owners:
- name: Matt Butcher
  email: technosophos@gmail.com
  homepage: http://technosophos.com
- name: Matt Farina
  email: matt@mattfarina.com
  homepage: https://www.mattfarina.com
ignore:
- appengine
excludeDirs:
- node_modules
import:
- package: gopkg.in/yaml.v2
- package: github.com/Masterminds/vcs
  version: ^1.2.0
  repo:    git@github.com:Masterminds/vcs
  vcs:     git
- package: github.com/codegangsta/cli
  version: f89effe81c1ece9c5b0fda359ebd9cf65f169a51
- package: github.com/Masterminds/semver
  version: ^1.0.0
testImport:
- package: github.com/arschles/assert
```
Again, some of the configurations are langauge specific, such as testImports, that is only installed when running tests for the project.


