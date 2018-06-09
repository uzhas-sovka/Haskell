# Haskell installation guide 2018 for Windows 7

1) Remove all previous Haskell installations. No need to clean registry, just use tools like Revo Uninstaller and manually delete folders **C:\Users\\{Name}\AppData\Roaming\Cabal** and **C:\Users\\{Name}\AppData\Roaming\Ghc** afterwards.

2) Install Git for Windows, https://git-scm.com/download/win. Check "Additional items on the Desktop" during installation, we will be using Git Bash a lot. Leave the rest as it is.

3) Install Haskell-ide-engine. Run Git Bash from desktop (you may enlarge font in Options/Text), then paste
  
    `git clone https://github.com/haskell/haskell-ide-engine --recursive`

    and press enter. Wait for operation to complete.

4) The rest
