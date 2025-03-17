1. https://code.visualstudio.com/docs/copilot/prompt-crafting
2. .github/copilot-instructions.md
3. https://github.com/microsoft/vscode/blob/main/.github/copilot-instructions.md
4. CTRL+SHIFT+P --> (remove >) -->  Settings.json
   ```json
   "github.copilot.chat.commitMessageGeneration.instructions" : [
      {
         "text" : "Be extremely deataield with the file chagnges and the reasong for the change. Add lot of emojis",
       }
   ]
   ```
5.  settings.json  (.vscode/settings.json) that overrides the internal vscode settings 
    ```json
    
   ```
7.  
