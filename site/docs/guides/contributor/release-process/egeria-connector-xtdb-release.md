<!-- SPDX-License-Identifier: CC-BY-4.0 -->
<!-- Copyright Contributors to the Egeria project 2020. -->

### XTDB Connector Release Process

#### Obtaining releases / artifacts for Core Egeria

| Location | Usage |
|---|---|
| [Maven Central connector release :material-dock-window:](https://mvnrepository.com/artifact/org.odpi.egeria){ target=maven } | typically used by other developers integrating with our code |
| [Github connector release :material-github:](https://github.com/odpi/egeria-connector-xtdb/releases){ target=gh } | source code in `zip` and `tar.gz` formats |
| `git` | `git checkout vx.y` to get version as-shipped (each release is tagged at the point it is shipped) |

### XTDB connector release process

??? success "1. Await core Egeria release"
    Connector release are done shortly after a corresponding Egeria core release. Any other changes to the connector are simply consolidated for the tandem release alongside Egeria core -- we do not do interim releases of the connector.

??? success "2. Track remaining issues and PRs"
    - Aim to branch when most issues / PRs are complete to minimize back-porting from master, but not at the expense of impacting ongoing master development

??? success "3. Create branch"
    - Checkout main `git checkout main`
    - Ensure local update `git fetch upstream`, `git merge upstream/main`, `git pull --no-rebase`
    - Create branch `git branch release-x.y`
    - Push to upstream `git push upstream release-x.y`

??? success "4. Update `release-x.y` from `x.y-SNAPSHOT` to `x.y`"
    - `git checkout release-x.y`
    - Edit all files (command line or IDE) to replace `x.y-SNAPSHOT` with the same non-snapshot version, e.g. change `1.3-SNAPSHOT` to `1.3`. Most of the changes are in `pom.xml` files, however some code and documentation also has references to our versions and all need modifying.
    - If using an IDE like IntelliJ, make sure you have all hits by searching again as [by default only a limited number of hits are shown :material-dock-window:](https://youtrack.jetbrains.com/issue/IDEA-157855){ target=intellij }.
    - Commit
    - Create a PR, have reviewed / approved and merged as usual - aim to do this as quickly as reasonable so that there is no potential for version clash

??? success "5. Test, merge any remaining required changes into branch"
    - Run appropriate tests for the release. For example, in addition to automated build tests:
        - Run the CTS and check that all profiles are compliant
        - If infrastructure exists, run the PTS and check that there are no unexpected performance regressions.
    - Raise issues for any changes required as usual.
        - If there are any issues, delete the `release-x.y` branch, fix in `main` branch, and repeat steps (3-4) until no remaining issues.

??? success "6. Update `main`s release version from `x.y-SNAPSHOT` to `x.z-SNAPSHOT`"
    - `git checkout main`
    - Ensure local update `git fetch upstream`, `git merge upstream/main`, `git pull --no-rebase`
    - Edit all files (command line or IDE) to replace `x.y-SNAPSHOT` with `x.z-SNAPSHOT`. Most of the changes are in `pom.xml` files; however, some code and documentation also has references to our versions and all need modifying.
    - Commit, and do not make any other changes.
    - Create a PR, have reviewed / approved and merged as usual

??? success "7. Create a release in GitHub"
    - [Create the GitHub release :material-github:](https://github.com/odpi/egeria-connector-xtdb/releases){ target=gh }. Use `vx.y` as the tag, and ensure the correct branch is set for the target, i.e. `release-x.y`
    - Fill in the release notes using a 1-3 word title summarizing the primary changes in the release and in the description outline the changes across new features, bug fixes, security fixes, any repository migration required, and minimum version of Egeria against which the connector should be used
    - Notify Nigel once the release is staged from GitHub -- he's the only person currently with access to then publish the release itself to Maven Central (usually takes around half a day once released from staging).
    - Source archives will be added to the release on GitHub.

--8<-- "snippets/abbr.md"
