# Installation

    ```
    [environment]::setEnvironmentVariable('SCOOP','D:\Applications\Scoop','User')
    $env:SCOOP='D:\Applications\Scoop'
  [environment]::setEnvironmentVariable('SCOOP_GLOBAL','F:\GlobalScoopApps','Machine')
    $env:SCOOP_GLOBAL='F:\GlobalScoopApps'
    iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
    ```
# Reset Application

```
scoop reset *
```