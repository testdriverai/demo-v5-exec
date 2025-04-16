# demo-v5-exec

New (undocumented) changes in v5:

# Lifecycle Scripts

Opening any instance of testdriver will automatically run script found in `testdriver/lifecycle/prerun.yaml`.

# Exec Updates

Exec now takes a `lang` argument and has support for different OSs thought (`linux`, `mac`, and `windows`).

- `lang` values are `js` or `shell`
  - `js` code is executed in a NodeJS VM on the `host` machine (your computer)
  - `shell` code is executed in shell on the `runner`.
- code found in `linux`, `mac`, and `windows` is run based on the platform of the `runner` machine 

```yaml
- command: exec
  lang: shell
  linux: |
    jumpapp google-chrome --disable-fre --no-default-browser-check --no-first-run "${TD_WEBSITE}" &
    exit
  mac: |
    open -na "Google Chrome" --args --disable-fre --no-default-browser-check --no-first-run --disable-features=PasswordManagerEnabled "${TD_WEBSITE}" &
    exit
  windows:
    Start-Process "C:/Program Files/Google/Chrome/Application/chrome.exe" -ArgumentList "--start-maximized", "${TD_WEBSITE}"
    exit
- command: wait-for-text
  text: "Google Chrome"
  timeout: 30000
```

# VM Updates

VMs are now customized with:
- `jumpapp`
- `nodejs`
- Google Chrome
- TestDriver wallpaper
