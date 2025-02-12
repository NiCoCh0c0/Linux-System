# APT (not Bruno Mars song)

## Update and Upgrade
When we want to update our system, we can easily use
```bash
apt update && apt upgrade
```
But how we need this two commands ?
### Apt update
In fact apt update fetch the lastest version of the package list from your distro's software repository and, if you configured it, from other thrid party repositories.
It will check the latest version of all packages and what are the dependencies. In fact, apt update will not download packages ! He just let the system know the avaible packages to download, their latest version and dependencies.

### Apt upgrade
Upgrade will check if the installed packages are up to date. You have to use apt update to perform this action correctly because apt update will let us know the lastest version of the packages. 
Btw, without apt update, the last version will be the version that was already installed. In reality, upgrade will not upgrade all the packages (if they need it). Upgrade command will perform the following steps :
- The update command updates the package list with the latest available versions
- It won't upgrade the installed packages just update the package list with a new version
- To update the already installed packages to the latest available version
- If the dependencies are missed the current version will be kept without any upgrade

In order to perform upgrade on packages which needs dependencies, we need another command : apt dist-upgrade

### Apt dist-upgrade
This command will act the same as the classic upgrade except on a point : it upgrade package with missing dependancies. So it will perform the same with some additions :
- It install requiered packages
- It removes the already installed packages to make the clear upgrade

It's a nice command on new system you need to upgrade.
That's cool to install requiered dependancies but what about the conflicts ? Some packages can use different version off a dependency. We can introduce new issues cause of it. It's probably time to full-upgrade.

### Apt full-upgrade
Full-upgrade will resolv all your conflict but it has a price : full-upgrade also remove installed packages if required to resolve a package conflict. If their isn't any conflict, it act list dist-upgrade

### Apt do-realese-upgrade
I mention it here beacause it exist. You use it only change the OS version (eg. ubuntu 18.04 to 20.04). The system has to be upgrade to use this command.

## Cache
### How apt use cache
When you install a package, apt will store the package on /var/cache/apt/archives (and store in /var/cache/apt/archives/partion during the installation). 
Why ? Because if you unistall the package and want to reinstall it, it will be faster ! The main problem of this method is the disk usage. So if you want to clear the cache you've got two options clean or autoclean.

PS : clear the cache is fully safe

### Apt clean
It complitely removes the cache in /var/cache/apt/archives directory (except lock files). If you want to keep the rapidity of cache and only remove useless packages you need autoclean

### Apt autoclean
Autoclean will clean /var/cache/apt/archives directory, like clean you will say, with a difference : only packages that are not possible to download will be removed. 
Like we saw on update, package can have different versions. So if a version is to old, you will probably will download it any more (you can on special case but it's a really specific).
So, you will lose nothing to delete it ;)

### Apt autoremove
It remove orphans package, nice to do because orphans are no longer needed for the system. Becarefull, it doesn't purge them ! You can use --purge to do this

### Cache conclusion
Even if you want to optimise you delete/re-install package, you win space without any issue this command :
sudo apt autoremove --purge && sudo apt clean
