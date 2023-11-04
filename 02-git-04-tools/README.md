1. Какому тегу соответствует коммит 85024d3?

<pre>
serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$ git describe --contains 85024d3
<b>v0.12.23^0</b>
serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$
</pre>


2. Сколько родителей у коммита b8d720? Напишите их хеши.

<pre>
serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$ git show --format="%P" b8d720
<b>b56cd7859e05c36c06b56d013b55a252d0bb7e158>56cd7859e05c36c06b56d013b55a252d0bb7e158 9ea88f22fc6269854151c571162c5bcf958bee2b</b>

serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$ git show --format=fuller b8d720
commit b8d720f8340221f2146e4e4870bf2ee0bc48f2d5
<b>Merge:>Merge: 56cd7859e0 9ea88f22fc</b>
Author:     Chris Griggs <cgriggs@hashicorp.com>
AuthorDate: Tue Jan 21 17:45:48 2020 -0800
Commit:     GitHub <noreply@github.com>
CommitDate: Tue Jan 21 17:45:48 2020 -0800

    Merge pull request #23916 from hashicorp/cgriggs01-stable

    [Cherrypick] community links

serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$
</pre>

3. Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами v0.12.23 и v0.12.24.

<pre>
serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$ git log --pretty=format:"%h %s" v0.12.23..v0.12.24
33ff1c03bb v0.12.24
b14b74c493 [Website] vmc provider links
3f235065b9 Update CHANGELOG.md
6ae64e247b registry: Fix panic when server is unreachable
5c619ca1ba website: Remove links to the getting started guide's old location
06275647e2 Update CHANGELOG.md
d5f9411f51 command: Fix bug when using terraform login on Windows
4b6d06cc5d Update CHANGELOG.md
dd01a35078 Update CHANGELOG.md
225466bc3e Cleanup after v0.12.23 release
serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$
</pre>

4. Найдите коммит, в котором была создана функция func providerSource, её определение в коде выглядит так: func providerSource(...) (вместо троеточия перечислены аргументы).

<pre>
serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$ git log -S 'func providerSource(' --oneline
<b>8c928e8358</b> main: Consult local directories as potential mirrors of providers

serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$ git show 8c928e8358
commit 8c928e83589d90a031f811fae52a81be7153e82f
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Thu Apr 2 18:04:39 2020 -0700

    main: Consult local directories as potential mirrors of providers

    This restores some of the local search directories we used to include when
    searching for provider plugins in Terraform 0.12 and earlier. The
    directory structures we are expecting in these are different than before,
    so existing directory contents will not be compatible without
    restructuring, but we need to retain support for these local directories
    so that users can continue to sideload third-party provider plugins until
    the explicit, first-class provider mirrors configuration (in CLI config)
    is implemented, at which point users will be able to override these to
:...skipping...
commit 8c928e83589d90a031f811fae52a81be7153e82f
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Thu Apr 2 18:04:39 2020 -0700

    main: Consult local directories as potential mirrors of providers

    This restores some of the local search directories we used to include when
    searching for provider plugins in Terraform 0.12 and earlier. The
    directory structures we are expecting in these are different than before,
    so existing directory contents will not be compatible without
    restructuring, but we need to retain support for these local directories
    so that users can continue to sideload third-party provider plugins until
    the explicit, first-class provider mirrors configuration (in CLI config)
    is implemented, at which point users will be able to override these to
    whatever directories they want.

    This also includes some new search directories that are specific to the
    operating system where Terraform is running, following the documented
    layout conventions of that platform. In particular, this follows the
    XDG Base Directory specification on Unix systems, which has been a
    somewhat-common request to better support "sideloading" of packages via
    standard Linux distribution package managers and other similar mechanisms.
    While it isn't strictly necessary to add that now, it seems ideal to do
    all of the changes to our search directory layout at once so that our
    documentation about this can cleanly distinguish "0.12 and earlier" vs.
    "0.13 and later", rather than having to document a complex sequence of
    smaller changes.

    Because this behavior is a result of the integration of package main with
    package command, this behavior is verified using an e2etest rather than
    a unit test. That test, TestInitProvidersVendored, is also fixed here to
    create a suitable directory structure for the platform where the test is
    being run. This fixes TestInitProvidersVendored.

diff --git a/command/e2etest/init_test.go b/command/e2etest/init_test.go
index 9fcddbfb72..3031695a7f 100644
--- a/command/e2etest/init_test.go
+++ b/command/e2etest/init_test.go
@@ -100,6 +100,16 @@ func TestInitProvidersVendored(t *testing.T) {
        tf := e2e.NewBinary(terraformBin, fixturePath)
        defer tf.Close()

+       // Our fixture dir has a generic os_arch dir, which we need to customize
+       // to the actual OS/arch where this test is running in order to get the
+       // desired result.
+       fixtMachineDir := tf.Path("terraform.d/plugins/registry.terraform.io/hashicorp/null/1.0.0+local/os_arch")
+       wantMachineDir := tf.Path("terraform.d/plugins/registry.terraform.io/hashicorp/null/1.0.0+local/", fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH))
+       err := os.Rename(fixtMachineDir, wantMachineDir)
+       if err != nil {
+               t.Fatalf("unexpected error: %s", err)
+       }
+
        stdout, stderr, err := tf.Run("init")
        if err != nil {
                t.Errorf("unexpected error: %s", err)
diff --git a/main.go b/main.go
index 762d566a52..f9a3b9cf80 100644
--- a/main.go
+++ b/main.go
@@ -17,7 +17,6 @@ import (
        "github.com/hashicorp/terraform/command/format"
        "github.com/hashicorp/terraform/helper/logging"
        "github.com/hashicorp/terraform/httpclient"
-       "github.com/hashicorp/terraform/internal/getproviders"
        "github.com/hashicorp/terraform/version"
        "github.com/mattn/go-colorable"
        "github.com/mattn/go-shellwords"
@@ -169,7 +168,7 @@ func wrappedMain() int {
        // direct from a registry. In future there should be a mechanism to
        // configure providers sources from the CLI config, which will then
        // change how we construct this object.
-       providerSrc := getproviders.NewRegistrySource(services)
+       providerSrc := <b>providerSource(services)>providerSource(services)</b>

        // Initialize the backends.
        backendInit.Init(services)
diff --git a/provider_source.go b/provider_source.go
new file mode 100644
index 0000000000..9524e09852
--- /dev/null
+++ b/provider_source.go
@@ -0,0 +1,89 @@
+package main
+
+import (
+       "log"
+       "os"
+       "path/filepath"
+
+       "github.com/apparentlymart/go-userdirs/userdirs"
+
+       "github.com/hashicorp/terraform-svchost/disco"
+       "github.com/hashicorp/terraform/command/cliconfig"
+       "github.com/hashicorp/terraform/internal/getproviders"
+)
+
+// <b>providerSource</b> constructs a provider source based on a combination of the
+// CLI configuration and some default search locations. This will be the
+// provider source used for provider installation in the "terraform init"
+// command, unless overridden by the special -plugin-dir option.
+func <b>providerSource(services>providerSource(services *disco.Disco)</b> getproviders.Source {
+       // We're not yet using the CLI config here because we've not implemented
+       // yet the new configuration constructs to customize provider search
+       // locations. That'll come later.
+       // For now, we have a fixed set of search directories:
+       // - The "terraform.d/plugins" directory in the current working directory,
+       //   which we've historically documented as a place to put plugins as a
+       //   way to include them in bundles uploaded to Terraform Cloud, where
+       //   there has historically otherwise been no way to use custom providers.
+       // - The "plugins" subdirectory of the CLI config search directory.
+       //   (thats ~/.terraform.d/plugins on Unix systems, equivalents elsewhere)
+       // - The "plugins" subdirectory of any platform-specific search paths,
+       //   following e.g. the XDG base directory specification on Unix systems,
+       //   Apple's guidelines on OS X, and "known folders" on Windows.
+       //
+       // Those directories are checked in addition to the direct upstream
+       // registry specified in the provider's address.
+       var searchRules []getproviders.MultiSourceSelector
+
+       addLocalDir := func(dir string) {
+               // We'll make sure the directory actually exists before we add it,
+               // because otherwise installation would always fail trying to look
+               // in non-existent directories. (This is done here rather than in
+               // the source itself because explicitly-selected directories via the
+               // CLI config, once we have them, _should_ produce an error if they
+               // don't exist to help users get their configurations right.)
+               if info, err := os.Stat(dir); err == nil && info.IsDir() {
+                       log.Printf("[DEBUG] will search for provider plugins in %s", dir)
+                       searchRules = append(searchRules, getproviders.MultiSourceSelector{
+                               Source: getproviders.NewFilesystemMirrorSource(dir),
+                       })
+               } else {
+                       log.Printf("[DEBUG] ignoring non-existing provider search directory %s", dir)
+               }
+       }
+
+       addLocalDir("terraform.d/plugins") // our "vendor" directory
+       cliConfigDir, err := cliconfig.ConfigDir()
+       if err != nil {
+               addLocalDir(filepath.Join(cliConfigDir, "plugins"))
+       }
+
+       // This "userdirs" library implements an appropriate user-specific and
+       // app-specific directory layout for the current platform, such as XDG Base
+       // Directory on Unix, using the following name strings to construct a
+       // suitable application-specific subdirectory name following the
+       // conventions for each platform:
+       //
+       //   XDG (Unix): lowercase of the first string, "terraform"
+       //   Windows:    two-level heirarchy of first two strings, "HashiCorp\Terraform"
+       //   OS X:       reverse-DNS unique identifier, "io.terraform".
+       sysSpecificDirs := userdirs.ForApp("Terraform", "HashiCorp", "io.terraform")
+       for _, dir := range sysSpecificDirs.DataSearchPaths("plugins") {
+               addLocalDir(dir)
+       }
+
+       // Last but not least, the main registry source! We'll wrap a caching
+       // layer around this one to help optimize the several network requests
+       // we'll end up making to it while treating it as one of several sources
+       // in a MultiSource (as recommended in the MultiSource docs).
+       // This one is listed last so that if a particular version is available
+       // both in one of the above directories _and_ in a remote registry, the
+       // local copy will take precedence.
+       searchRules = append(searchRules, getproviders.MultiSourceSelector{
+               Source: getproviders.NewMemoizeSource(
+                       getproviders.NewRegistrySource(services),
+               ),
+       })
+
+       return getproviders.MultiSource(searchRules)
+}
(END)

</pre>

5. Найдите все коммиты, в которых была изменена функция globalPluginDirs.

<pre>
serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$ git log -S 'globalPluginDirs' --oneline
65c4ba7363 Remove terraform binary
125eb51dc4 Remove accidentally-committed binary
22c121df86 Bump compatibility version to 1.3.0 for terraform core release (#30988)
7c7e5d8f0a Don't show data while input if sensitive
35a058fb3d main: configure credentials from the CLI config file
c0b1761096 prevent log output during init
8364383c35 Push plugin discovery down into command package
serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$ 
</pre>

6. Кто автор функции synchronizedWriters?

<pre>
serg@wsl-hyper-vm:/mnt/c/gitwork/terraform$ git log -S 'synchronizedWriters'
commit bdfea50cc85161dea41be0fe3381fd98731ff786
Author: James Bardin <j.bardin@gmail.com>
Date:   Mon Nov 30 18:02:04 2020 -0500

    remove unused

commit fd4f7eb0b935e5a838810564fd549afe710ae19a
Author: James Bardin <j.bardin@gmail.com>
Date:   Wed Oct 21 13:06:23 2020 -0400

    remove prefixed io

    The main process is now handling what output to print, so it doesn't do
    any good to try and run it through prefixedio, which is only adding
    extra coordination to echo the same data.

commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5
<b>Author: Martin Atkins <mart@degeneration.co.uk></b>
Date:   Wed May 3 16:25:41 2017 -0700

    main: synchronize writes to VT100-faker on Windows

    We use a third-party library "colorable" to translate VT100 color
    sequences into Windows console attribute-setting calls when Terraform is
    running on Windows.

    colorable is not concurrency-safe for multiple writes to the same console,
    because it writes to the console one character at a time and so two
    concurrent writers get their characters interleaved, creating unreadable
    garble.

    Here we wrap around it a synchronization mechanism to ensure that there
    can be only one Write call outstanding across both stderr and stdout,
    mimicking the usual behavior we expect (when stderr/stdout are a normal
    file handle) of each Write being completed atomically.
</pre>


