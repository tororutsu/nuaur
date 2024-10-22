# Local Repo Management Script

This script is designed for managing signed AUR (Arch User Repository) packages in a local repo using Nushell. It provides functions for building packages, signing them, and searching for packages in the AUR.

## Prerequisites

- **Nushell**: Install Nushell on your system.
- **Git**: Required for cloning AUR repositories.
- **GPG**: GNU Privacy Guard for signing packages.
- **makechrootpkg**: Tool for building packages in a clean chroot environment.
- **repo-add**: Utility for maintaining Arch Linux package repositories.

### Environment

Please set the `$env.NUAURBUILD & $env.NUAURPKG` paths for optimal use. 

## Functions

### `main build`

Builds AUR packages located in a specified directory.

#### Parameters:
- `builddir`: (Optional) Path to the directory containing AUR packages (default: `$env.NUAURBUILD`).

#### Description:
- Changes to the `builddir`.
- Lists all directories in the `builddir` and iterates over each one.
- Changes to each directory and runs `makechrootpkg` to build the package.
- Prints a reminder to sign the packages after building.

### `main sign`

Signs the built packages and updates the repository database.

#### Parameters:
- `pkgdir`: (Optional) Path to the directory where built packages are stored (default: `$env.NUAURPKG`).

#### Description:
- Changes to the `pkgdir`.
- Lists `.zst` files (compressed package files) that do not have a corresponding `.sig` file.
- Signs each package using GPG.
- Adds the signed packages to the repository database and signs the database using `repo-add`.

### `main search`

Searches for packages in the AUR or fetches the package repository.

#### Parameters:
- `package`: Name of the package to search for or fetch.
- `--fetch`: Flag indicating whether to fetch (clone) the package repository.

#### Description:
- If the `--fetch` flag is set, clones the package repository from AUR.
- If `--fetch` is not set, performs a search for the package using AUR RPC and returns the names of the search results.

## To-Do

- [ ] **Add Error Handling:** Implement error handling for cases where commands fail or directories are not found.
- [/] **Configuration File:** Allow configuration of `builddir` and `pkgdir` through a configuration file instead of hardcoded paths.
        - Got rid of hardcoded paths for environment variables. Still thinking about a config file.
- [ ] **Logging:** Add logging functionality to track the build and sign process, including success and failure messages.
- [ ] **Tests:** Write tests to ensure each function behaves as expected under various scenarios.
- [ ] **Documentation:** Expand documentation to include detailed explanations of each function and example use cases.
- [ ] **User Input Validation:** Add validation for user inputs to ensure they are correct and handle invalid inputs gracefully.
- [ ] **Automation:** Consider automating the process of updating the repository and signing packages on a schedule.

