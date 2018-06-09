# Haskell installation guide 2018 for Windows 7

1) Remove all previous Haskell installations. No need to clean registry, just use tools like Revo Uninstaller and manually delete folders **C:\Users\\{Name}\AppData\Roaming\Cabal** and **C:\Users\\{Name}\AppData\Roaming\Ghc** afterwards.

2) Install Git for Windows, https://git-scm.com/download/win. Check "Additional items on the Desktop" during installation, we will be using git-bash a lot. Leave the rest as it is.

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
    cd d:/haskell
    stack new ToyProject simple
    cd ToyProject
    stack setup
    stack build
    stack exec ToyProject
    ```
    The output has to be `"hello world"`
    Keep git-bash running.
    
8) Add package to ToyProject. Go to D:\Haskell\ToyProject\Main.hs and change contents of the file to

   ```
   module Main where

   import Data.String.Utils

   main :: IO ()
   main = print $ replace "5" "6" "555"
   ```
   Open `D:\Haskell\ToyProject\ToyProject.cabal` and change string
   `build-depends: base >= 4.7 && < 5`
   to 
   `build-depends: base >= 4.7 && < 5, MissingH`.
   
   In git-bash run
   ```
   stack build
   stack exec ToyProject
   ```
   The output has to be `666`.
   
 9) Install Atom text editor.
 10) In git-bash run
 
     `apm install language-haskell atom-ide-ui ide-haskell-hie script`
     
 11) Patch Script package in Atom. Choose File/Settings/Packages, enter Script, wait for Script box to appear, click Settings/View code.      At the left tree choose script/lib/grammars/haskell.coffee. Change 'File Based' part to

      ```
      'File Based':
        command: 'stack'
        args: ({filepath}) ->
        parts = filepath.split('\\')
        projectName = parts[2]
        return ['build', '--exec', projectName]
       ```
       Close haskell.coffee tab, click "save", close Atom.
   
 12) Create .bat file with `@stack exec -- hie %*` and save it not far from your Haskell folder.
 13) Launch Atom, go to ide-haskell-hie package settings, scroll down, check the box "Use a custom hie wrapper" and write the path to          your bat file in the input field below (for example `D:\Haskell\wrapper.bat`).
 14) Re-launch Atom. Open folder `D:\Haskell\ToyProject` (open folder, not file). Navigate to `src\Main.hs`, open `Main.hs`. Click            `ctrl+shift+b`. The output has to be `666`.
 15) Generate haddock documentation for ToyProject. In git-bash run
     ```
     cd D:/Haskell/ToyProject
     stack haddock --keep-going
     ```
 16) Generate hoogle database. In git-bash run
     ```
     cd C:/Hie
     stack --stack-yaml=stack.yaml exec hoogle generate
     ```

## Thanks a lot to  @worker4food, Anonim Legion, @haskellru and Testov Testov for the idea of "Stone Axe"
