## Integrate with PHPStorm
Here are the steps to set up StandardJS in PhpStorm:
1.  Install StandardJS: You can install StandardJS globally by running `npm install standard -g`
2.  Open PhpStorm and go to "Preferences" (or "Settings" in Windows)
3.  Select "Languages & Frameworks" > "JavaScript" > "Code Quality Tools"
4.  In the right panel, click the "+" button to add a new StandardJS configuration.
5.  Choose "StandardJS" from the list.
6.  In the "Node Interpreter" field, select the node binary that was installed when you installed StandardJS.
7.  In the "JavaScript Standard Style Configuration" field, enter the path to your local `.standardrc` file.
8.  In the "Options" field, you can add additional arguments for the StandardJS command. For example, `--fix` to automatically fix any linting issues.
9.  Apply the changes and close the preferences window.
10.  Now, you can use StandardJS in PhpStorm by opening a .js file and using the Code > Run StandardJS action from the menu, or by pressing `Ctrl + Alt + S`.

## Resource 
- [Official Website](https://standardjs.com/)