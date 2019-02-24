rudo
====
rudo is a toy `sudo` clone written in [Rust](http://www.rust-lang.org/) that aims to serve as a learning tool as well as (potentially) a useful system administration tool.

**DISCLAIMER: This is a toy. This has not undergone any formal security analysis. I am not a security expert. Use at your own risk.**

Why?
----
I wanted to learn Rust by writing a project that would highlight its strengths as a safe systems programming language. Many other command-line utilities have been rewritten in Rust, but to my knowledge `sudo` has not.

Eventually, rudo may reach a high level of security and usability and become useful as a system administration tool, but for now it's mostly an experiment.

Supported Platforms
-------------------
rudo has been tested on both Linux and macOS, but it should work on any *nix with PAM.

Automatic Installation
----------------------
To automatically install rudo, simply clone the repository and run the included `install.sh` as root. Note that you will need a Rust environment (I recommend using [rustup](https://rustup.rs)) as well as the PAM header files for your system.
```
$ git clone https://github.com/shawnanastasio/rudo
# ./install.sh
```
Once the installation is complete, you can edit the configuration file at `/etc/rudo.json` to include your user.

### Example:
```
{
  "prompt": "Password: ",
  "allowed_users": [
    {
      "username": "root",
      "permissions": { "allowed_commands": [ "*" ] }
    },
    {
      "username": "shawnanastasio",
      "permissions": { "allowed_commands": [ "whoami", "ls" ] }
    }
  ]
}
```

To enable (experimental) TouchID on newer macs, call `./install.sh` with `--features macos_extra`:
```
# ./install.sh --features macos_extra
```
Once the feature is enabled, rudo will attempt to authenticate with TouchID. If TouchID authentication fails, rudo will fall back to PAM password authentication.

Manual Installation
-------------------
See `install.sh` for full list of steps.



TODO
----
* Add more granular control over permissions system
* Make configuration file less ugly

License
-------
All code is licensed under the MIT license. See `LICENSE` for more information.

Fork Me
-------
Pull requests and suggestions are welcome!
