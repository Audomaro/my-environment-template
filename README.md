# Environment files

The provided script enables the creation of symbolic links for specified files like .bashrc, .gitconfig, among others, facilitating the synchronization of these configuration files across different machines used by the developer. This synchronization is achieved through the use of a Git repository, ensuring consistent settings and preferences across various environments.

## File configuration

This is the structure of the config.env file. It is recommended to add $(pwd) as a prefix to the file paths so that the script resolves the correct path. Additionally, it is important to use ":" to indicate the source and destination paths.

  Example :

  ```text
  $(pwd)/files/.bashrc:$HOME/.bashrc
  $(pwd)/files/.gitconfig:$HOME/.gitconfig
  ```

  > In Linux, the environment variable **$HOME** and the tilde character **~** are equivalent and represent the user's home directory.

## How to use

Below is a description of the process to follow for configuring the files.

- Include the path of the file and its corresponding path for symbolic.

- Run the script

  ```bash
  ./myenv [options]
  ```

| Option           | Description                                                                                    |
|------------------|------------------------------------------------------------------------------------------------|
| `--add-to-env`   | Append the script's path to the end of the .bashrc file to include it in the PATH environment. |
| `--configure`    | Generate symbolic links for the designated files listed in the 'env.config' file.              |
| `--print-config` | Prints the list of files and their symbolic links.                                             |
| `--remove`       | Remove symbolic links for the files specified in the 'env.config' file.                        |
| `--sync`         | Pull and push changes from the repository.                                                     |
| `-h, --help`     | Print help.                                                                                    |

> Notes: It may require access to run in the case of the Linux-based operating system
> Used ```chmod +x ./myenv``

## Recommendations

### To this tool

- I recommend using the ```--add-to-env``` option so that 'myenv' command is accessible from any location.

### Multiple configurations for Git

It is recommended to use different configurations based on the folder path where the repositories are located. This allows for using a specific account and configuration, for example, work, and another one for personal projects. This can be achieved as follows (the following example applies to Windows users):

Main configuration in .gitconfig

```.gitconfig
[user]
  name = Personal
  email = personal@email.com

# Here it is specified that when the path is the designated one, it should use the configuration from 'work.gitconfig
[includeIf "gitdir/i:C:/work_repos/**"] 
  path = work.gitconfig

[core]
  editor = \"$USERPROFILE/AppData/Local/Programs/Microsoft VS Code/bin/code\" --wait
```

Configuration of the 'work.gitconfig' file:

```.gitconfig
[user]
  name = Work
  email = work@email.com
```
