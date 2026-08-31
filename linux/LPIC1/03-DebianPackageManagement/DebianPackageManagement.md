# Debian Package Management 

## 1. High-Level vs Low-Level Package Tools

* **`dpkg` (Low-Level)**: Installs and extracts local `.deb` files. Does **not** resolve or download external dependencies from internet repositories.
* **`apt` / `apt-get` (High-Level)**: Dependency managers that query remote repositories, calculate dependency trees, download necessary `.deb` files, and pass them to `dpkg` for installation.

---

## 2. Low-Level Package Management with `dpkg`

| Command / Flag | Description |
| :--- | :--- |
| `dpkg -i package.deb` | Install or upgrade a local `.deb` package |
| `dpkg -r package_name` | Remove package (leaves configuration files intact) |
| `dpkg -P package_name` | **Purge** package (removes both the binary and configuration files) |
| `dpkg -l [pattern]` | List installed packages matching pattern |
| `dpkg -L package_name` | List all files installed on the system by `package_name` |
| `dpkg -S /path/to/file` | Find which installed package owns the specified file |
| `dpkg -s package_name` | Display package status and metadata (version, dependencies) |
| `dpkg -c package.deb` | List contents of an **uninstalled** `.deb` archive |
| `dpkg-reconfigure pkg` | Re-run the interactive configuration setup for an installed package |

---

## 3. High-Level Package Management with `apt` & `apt-cache`

| Command | Description |
| :--- | :--- |
| `apt update` | Resynchronize package index files from sources (does not upgrade software) |
| `apt upgrade` | Upgrade all installed packages to their newest versions |
| `apt full-upgrade` / `dist-upgrade` | Upgrade packages, smartly handling dependency changes (may install/remove packages) |
| `apt install package_name` | Download and install package and its dependencies |
| `apt remove package_name` | Remove package while keeping its config files |
| `apt purge package_name` | Remove package and delete its global config files |
| `apt autoremove` | Remove orphaned packages (installed as dependencies but no longer needed) |
| `apt clean` | Clear out local repository cache of retrieved package files (`/var/cache/apt/archives/`) |
| `apt search keyword` | Search for packages matching keyword in name or description |
| `apt show package_name` | Show package details (description, version, maintainer, dependencies) |
| `apt-cache depends package` | List all direct dependencies required by a package |
| `apt-cache rdepends package` | List all packages that depend on this package (reverse dependencies) |
| `apt-file search filename` | Search which remote package contains a specific file (requires `apt-file` installed) |

---

## 4. APT Repositories & Configuration

* **Main Repository File**: `/etc/apt/sources.list`
* **Modular Repositories**: `/etc/apt/sources.list.d/*.list` (preferred standard for third-party repos like Docker, NodeSource)

