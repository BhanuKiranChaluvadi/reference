This file explain how to configure the twincat project and make a version control

Resources:
1. [tc-source-control-tips](https://cookncode.com/twincat/2021/06/07/tc-source-control-tips.html)
2. [Beckhoff source control](https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_sourcecontrol/767894795.html&id=9000520481371853523)
3. [pre commit hook](https://cookncode.com/twincat/2022/04/14/pre-commit.html)
4. [TcBlack](https://github.com/Roald87/TcBlack/blob/master/docs/style.md)


Steps:
1. Add .gitignore file to the solution. You can find the .gitignore file from [here](https://github.com/BhanuKiranChaluvadi/tc3_visual_studio_gitignore).
2. Configure git to use Twincat Project Compare instead of regualr text file  compare
3. Configure Twincat XAE Shell to remove LineID .
4. Configure Twincat XAE Shell to create independent files.
5. Pin the Beckhoff libraries version
6. Pin the compile version
7.  Install remote manager of appropriate version to match the same runtime version as the target.
