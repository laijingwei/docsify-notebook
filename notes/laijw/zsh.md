# oh-my-zsh

### 安装

```bash
yum update && yum -y install zsh

sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# 配置文件
vim ~/.zshrc

plugins=(
  git
  npm
  yarn
  bower
  yarn
  yum
)

# 查看shell列表
cat /etc/shells

# 切换shell为zsh
chsh -s /bin/zsh
```

### Aliases

| Alias     | Command                                              | Description                                                     |
| --------- | ---------------------------------------------------- | --------------------------------------------------------------- |
| ys        | `yum search`                                         | Search package                                                  |
| yp        | `yum info`                                           | Show package info                                               |
| yl        | `yum list`                                           | List packages                                                   |
| ygl       | `yum grouplist`                                      | List package groups                                             |
| yli       | `yum list installed`                                 | Print all installed packages                                    |
| ymc       | `yum makecache`                                      | Rebuild the yum package list                                    |
| yu        | `sudo yum update`                                    | Upgrade packages                                                |
| yi        | `sudo yum install`                                   | Install package                                                 |
| ygi       | `sudo yum groupinstall`                              | Install package group                                           |
| yr        | `sudo yum remove`                                    | Remove package                                                  |
| ygr       | `sudo yum groupremove`                               | Remove pagage group                                             |
| yrl       | `sudo yum remove --remove-leaves`                    | Remove package and leaves                                       |
| yc        | `sudo yum clean all`                                 | Clean yum cache                                                 |
| gaa       | git add --all                                        |                                                                 |
| gcmsg     | git commit -m                                        |                                                                 |
| gp        | git push                                             |                                                                 |
| ggpush    | git push origin "$(git_current_branch)"              |                                                                 |
| gpsup     | git push --set-upstream origin $(git_current_branch) |                                                                 |
| gst       | git status                                           |                                                                 |
| gl        | git pull                                             |                                                                 |
| ggl       | git pull origin $(current_branch)                    |                                                                 |
| gpristine | git reset --hard && git clean -dfx                   |                                                                 |
| y         | `yarn`                                               | The Yarn command                                                |
| ya        | `yarn add`                                           | Install a package in dependencies (`package.json`)              |
| yad       | `yarn add --dev`                                     | Install a package in devDependencies (`package.json`)           |
| yap       | `yarn add --peer`                                    | Install a package in peerDependencies (`package.json`)          |
| yb        | `yarn build`                                         | Run the build script defined in `package.json`                  |
| ycc       | `yarn cache clean`                                   | Clean yarn's global cache of packages                           |
| yga       | `yarn global add`                                    | Install packages globally on your operating system              |
| ygls      | `yarn global list`                                   | Lists global installed packages                                 |
| ygrm      | `yarn global remove`                                 | Remove global installed packages from your OS                   |
| ygu       | `yarn global upgrade`                                | Upgrade packages installed globally to their latest version     |
| yh        | `yarn help`                                          | Show help for a yarn command                                    |
| yi        | `yarn init`                                          | Interactively creates or updates a package.json file            |
| yin       | `yarn install`                                       | Install dependencies defined in `package.json`                  |
| yls       | `yarn list`                                          | List installed packages                                         |
| yout      | `yarn outdated`                                      | Check for outdated package dependencies                         |
| yp        | `yarn pack`                                          | Create a compressed gzip archive of package dependencies        |
| yrm       | `yarn remove`                                        | Remove installed packages                                       |
| yrun      | `yarn run`                                           | Run a defined package script                                    |
| ys        | `yarn serve`                                         | Start the dev server                                            |
| yst       | `yarn start`                                         | Run the start script defined in `package.json`                  |
| yt        | `yarn test`                                          | Run the test script defined in `package.json`                   |
| yuc       | `yarn global upgrade && yarn cache clean`            | Upgrade global packages and clean yarn's global cache           |
| yui       | `yarn upgrade-interactive`                           | Prompt for which outdated packages to upgrade                   |
| yup       | `yarn upgrade`                                       | Upgrade packages to their latest version                        |
| `npmg`    | `npm i -g`                                           | Install dependencies globally                                   |
| `npmS`    | `npm i -S`                                           | Install and save to dependencies in your package.json           |
| `npmD`    | `npm i -D`                                           | Install and save to dev-dependencies in your package.json       |
| `npmE`    | `PATH="$(npm bin)":"$PATH"`                          | Run command from node_modules folder based on current directory |
| `npmO`    | `npm outdated`                                       | Check which npm modules are outdated                            |
| `npmV`    | `npm -v`                                             | Check package versions                                          |
| `npmL`    | `npm list`                                           | List installed packages                                         |
| `npmL0`   | `npm ls --depth=0`                                   | List top-level installed packages                               |
| `npmst`   | `npm start`                                          | Run npm start                                                   |
| `npmt`    | `npm test`                                           | Run npm test                                                    |
| `npmR`    | `npm run`                                            | Run npm scripts                                                 |
| `npmP`    | `npm publish`                                        | Run npm publish                                                 |
| `npmI`    | `npm init`                                           | Run npm init                                                    |
| bi        | `bower install`                                      | Installs the project dependencies listed in bower.json          |
| bl        | `bower list`                                         | List local packages and possible updates                        |
| bs        | `bower search`                                       | Finds all packages or a specific package.                       |


### Commands

| Command               | Description                                                                                                                  |
| :-------------------- | :--------------------------------------------------------------------------------------------------------------------------- |
| _tabs_                | Create a new tab in the current directory (macOS - requires enabling access for assistive devices under System Preferences). |
| _take_                | Create a new directory and change to it, will create intermediate directories as required.                                   |
| _x_ / _extract_       | Extract an archive (supported types: tar.{bz2,gz,xz,lzma}, bz2, rar, gz, tar, tbz2, tgz, zip, Z, 7z).                        |
| _zsh_stats_           | Get a list of the top 20 commands and how many times they have been run.                                                     |
| _uninstall_oh_my_zsh_ | Uninstall Oh-my-zsh.                                                                                                         |
| _upgrade_oh_my_zsh_   | Upgrade Oh-my-zsh.                                                                                                           |
| source ~/.zshrc       | Uptake new changes                                                                                                           |

---

| Alias   | Command                               |
| :------ | :------------------------------------ |
| _alias_ | list all aliases                      |
| ..      | cd ..                                 |
| ...     | cd ../..                              |
| ....    | cd ../../..                           |
| .....   | cd ../../../..                        |
| /       | cd /                                  |
| ~       | cd ~                                  |
| _cd +n_ | switch to directory number `n`        |
| _1_     | cd -                                  |
| _2_     | cd -2                                 |
| _3_     | cd -3                                 |
| _4_     | cd -4                                 |
| _5_     | cd -5                                 |
| _6_     | cd -6                                 |
| _7_     | cd -7                                 |
| _8_     | cd -8                                 |
| _9_     | cd -9                                 |
| _md_    | mkdir -p                              |
| _rd_    | rmdir                                 |
| _d_     | dirs -v (lists last used directories) |

See `~/.oh-my-zsh/lib/directories.zsh`