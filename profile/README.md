<p align="center">
  <a href="https://path-rc.com"><img src="banner.png" alt="path-rc" width="720"></a>
</p>

<p align="center">
  <b>Your shell, set up for the directory you're in.</b><br>
  Per-directory environment variables, aliases and <code>PATH</code> for bash, zsh and fish,
  with secrets encrypted by <a href="https://age-encryption.org">age</a>.
</p>

<p align="center">
  <a href="https://path-rc.com">path-rc.com</a> ·
  <a href="https://github.com/path-rc/pathrc">pathrc</a> ·
  <a href="https://github.com/path-rc/pathrc/releases">Releases</a> ·
  <a href="https://github.com/path-rc/pathrc/security/advisories/new">Report a vulnerability</a>
</p>

---

`pathrc` sets variables, aliases and `PATH` entries as you `cd` into a project,
and takes them away again when you leave. Each directory can hold a
`.pathrc.toml`; a sub-directory overrides just what differs.

```toml
# aws-project/.pathrc.toml
[common]
env.AWS_REGION = "eu-west-2"
alias.tfp = "terraform plan"

# aws-project/prod/.pathrc.toml.age, encrypted with age
[common]
env.AWS_ACCOUNT_ID = "111111111111"
env.AWS_REGION = "eu-west-1"
```

- **Encrypted with age.** A `.pathrc.toml.age` is decrypted in memory with
  your age or SSH key, for everyone in the nearest `.pathrc-recipients`.
- **Undone when you leave.** Variables are unset and overridden values come
  back, so nothing from project A leaks into project B.
- **Nothing runs until allowed.** A file applies only after `pathrc allow`,
  and again after every change.

### Install

```shell
curl -fsSL https://path-rc.com/install.sh | sh
eval "$(pathrc init)"   # in ~/.bashrc or ~/.zshrc; fish: pathrc init fish | source
```

Linux (x86-64, arm64) and macOS (Intel, Apple Silicon). BSD-3 licensed.
