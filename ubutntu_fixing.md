### Purging Packages

This is a very general answer to the question about the effects of purging packages. For advice specific to your situation, you'll have to edit your question to include additional information--in particular, the complete and exact text of the error message you are getting.

Removing packages with sudo apt purge ... or sudo apt --purge remove ... will remove them and all their global (i.e., systemwide) configuration files. This is usually what people mean when they talk about completely removing a package.

But that doesn't mean your system is the same as it was before the package was installed. In particular:

This does not remove packages that were installed as dependencies, when you installed the package you're now removing. Assuming those packages aren't dependencies of any other packages, and that you haven't marked them as manually installed, you can remove the dependencies with sudo apt autoremove or (if you want to delete their systemwide configuration files too) sudo apt --purge autoremove.

This does not remove non-systemwide configuration files. Specifically, it does not remove user-specific configuration:

It does not remove the configuration files and directories located in users' home directories (or in the .config subdirectory of their home directories), created by the software the package provides.
If these files/folders are not stored in .config, they usually start with a . themselves. Either way, you can see them with ls by using the -a or -A flag, and you can see them in Nautilus and most other file browsers/managers by pressing Ctrl+H or going to View > Show Hidden Files.

It does not reverse changes made to existing user-specific configuration files.

It does not remove new gconf or dconf keys, or reverse any gconf or dconf configuration changes.

Using purge or --purge remove instead of remove does not reverse changes to existing systemwide configuration files provided by other packages or created manually by the user. However, sometimes such changes are undone by uninstalling the package (whether or not it's a purge rather than a remove).

