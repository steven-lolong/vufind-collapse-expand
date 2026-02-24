# Versioning

This is still an ongoing discussion and might be changed until the first release is made!

## Basic Relation to VuFind-Versions
Since this module is only usable together with VuFind, we need to make it clear with which VuFind version the current module version will be compatible.
Of course we could define our own independant versioning scheme (starting with 1.0.0, then following basic rules of semantic versioning), and define a mapping which of our releases is compatible to which VuFind Version.

**BUT** - assume the following situation:
- We create a first release 1.0.0, which is compatible with VuFind 10.2
- We create a second release 1.1.0 (maybe 2.0.0), which is compatible with VuFind 11.0
- Now we want to release backports for VuFind 9.0 and 9.1 - which version would that be? (0.9.1 and 0.9.0? How to indicate updates within that version?)

**=> Conclusion 1)** It might cause less confusion if our versioning scheme contains the VuFind version as well as our own version.

## Compatibility with Minor/Major VuFind Versions

VuFind is using basic semantic versioning (X.Y.Z). Regarding compatibility and breaking changes, it should be enough to consider major releases in X. However, it happened in the past that breaking changes were introduced in minor versions Y as well.
We assume that Z will only contain bugfixes and never be affected by compatibility issues.

**=> Conclusion 2)** Our versioning schema should at least relate to version X.Y as a minimum.

## Version length / precision

Regarding our own Versioning: If we only add A as our own version (X.Y.A), this will not give any information to the user if there are only bugfixes, or breaking changes need to be addressed by their own custom extensions.

**=> Conclusion 3)** We should at least add A.B to the version number

## Options / Concrete proposals

So basically there are 2 suggestions:

**Option 1) X.Y.Z.A.B.C** => 10.2.0.1.0.0 => compatible with VuFind 10.2.0 in our module version 1.0.0
    - Very long, but very precise
    - Might allow auto-updates on user side, but might need more maintenance on our side
      (e.g. if we have a 10.2.0.1.0.0 and VuFind 10.2.1 is released, strictly we also need to release a 10.2.1.1.0.0 even though there are no differences in the code)

**Option 2) X.Y.A.B** => 10.2.1.0 => compatible with VuFind 10.2 in our module version 1.0
    - a compromise containing basically all necessary information
    - Might lead to B being increased for minor and bugfix versions alike
    - Might allow good auto-versioning for the end-user, by specifying e.g. "10.2.1.*" or "10.2.2.*" as dependency

## Variants / Open considerations
- Delimiter: X.Y.A.B => X.Y-A.B Is it possible to use a different delimiter to separate the two software versions, or would this cause side effects regarding the [composer versioning scheme](https://getcomposer.org/doc/articles/versions.md)?
- Sequence: X.Y.A.B => A.B.X.Y Should we move the VuFind Version to the end, e.g. 1.0.10.2? However this might cause expectations for the same module version to have exactly the same features across all VuFind-versions, even if some features might change due to altered Solr/VuFind versions. Also it might be a bad idea because you cannot specify proper versioning statements ("1.*.10.2" might not work assuming * needs to be at the end)
