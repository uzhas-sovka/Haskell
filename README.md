# Haskell installation guide 2018 for Windows 7

1) Remove all previous Haskell installations. No need to clean registry, just use tools like Revo Uninstaller and manually delete folders **C:\Users\\{Name}\AppData\Roaming\Cabal** and **C:\Users\\{Name}\AppData\Roaming\Ghc** afterwards.

2) Install Git for Windows, https://git-scm.com/download/win. Check "Additional items on the Desktop" during installation, we will be using Git Bash a lot. Leave the rest as it is.

3) Install Haskell-ide-engine. Run Git Bash from desktop (you may enlarge font in Options/Text), then paste
  
    `git clone https://github.com/haskell/haskell-ide-engine --recursive`

    and press enter. Wait for operation to complete.

4) Exit git-bash. Find folder **C:\msys\1.0\home\haskell-ide-engine** and copy (don't move) it to the root of drive C. Rename it from "haskell-ide-engine" to "hie".
5) Install Haskell Stack, https://docs.haskellstack.org/en/stable/README/#how-to-install.
6) Build `hie`. Launch git-bash, in git-bash run

    ```
    cd c:/hie
    stack build --copy-compiler-tool
    ```
    It takes maybe 20 minutes to complete.
 
 7) Make toy Haskell project. For example, your (now empty) root folder for Haskell projects is `D:\Haskell`. In git-bash run 
    
    ```
    cd d:/haskell/ToyProject
    stack new ToyProject simple
    ```
8) Keep git-bash runing. Build toy haskell project. In git-bash run

   `stack build`

   Wait for 10 minutes.
