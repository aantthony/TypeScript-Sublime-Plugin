TypeScript Plugin for Sublime Text
==================================

The plugin uses an IO wrapper around the TypeScript language services to provide
an enhanced Sublime Text experience when working with TypeScript code.

Installation
------------
If using [Package Control](https://packagecontrol.io/) for Sublime Text, simply 
install the `TODO` package.  

Alternatively, you can clone the repo directly into
your Sublime plugin folder.  For example, for Sublime Text 3 on a Mac this would 
look something like:

```
cd ~/"Library/Application Support/Sublime Text 3/Packages"
git clone https://github.com/Microsoft/TypeScript-Sublime-Plugin.git TypeScript
```

Platform support
----------------
The plugin has identical behavior across Windows, Mac, and Linux
platforms.  On Windows with ST2, you may see a "plugin delay" message
upon startup.  This happens because ST2 does not call "plugin_loaded()",
so the TypeScript server process is started from within an event handler.
Where possible, the use of a [Sublime Text 3](http://www.sublimetext.com/3) 
build >= 3070 is recommended, as this provides a popup API used for tool tips.

Features
--------
The below features are available via the keyboard shortcuts shown, or via the 
Command Pallete:

|Feature           | Shorcut       |
|------------------|---------------|
|Rename            | ^T ^M         |
|Find references   | ^T ^R         |
|Next reference    | ^T ^N         |
|Prev reference    | ^T ^P         |
|Format document   | ^T ^F         |
|Format selection  | ^T ^F         |
|Format line       | ^ ;           |
|Format braces     | ^ Shift + ]   |
|Go to definition  | ^T ^D (or F12)|
|Paste and format  | (^ or Super) V|
|Quick info        | ^T ^Q         |
|Rename            | ^T ^M         |

The plugin supports representing a TypeScript project via a 
[tsconfig.json](https://github.com/Microsoft/TypeScript/pull/1692) file. If a 
file of this name is detected in a parent directory, then its settings will be 
used by the plugin.

Issues
-------
The plugin is currently an Alpha, and as such there are many enhancements to 
implement, and many bugs to be fixed.  These are being tracked via the 
[GitHub Issues](https://github.com/Microsoft/TypeScript-Sublime-Plugin/issues) 
page for the project, and tagged with the appropriate issue type.

Please do log issues for any bugs you find or enhancements you would like to see 
(after searching to see if such as issue already exists).  We are excited to 
get your feedback and work with the community to make this plugin as awesome as 
possible.

Tips
----
1. Sublime Text 3 does not inform plug-ins of all buffer changes.  We
   are still learning how to detect changes in all cases.  If the view
   contents is out-of-sync with the server, you can re-sync by running
   the Undo command once.  The usual way to notice out-of-sync content
   is to see a surprising error message.
2. Snippets may contain text fields, which are placeholders within the
   snippet. The presence of text fields changes the key binding
   context and may temporarily turn off some of the TypeScript key
   bindings.  You can exit all snippet text fields by hitting the
   escape key.  You can tab from one text field to the next until you
   have exhausted the text fields (possibly filling them in along the way).
3. The server does not yet have file watch support for tsconfig.json
   projects.  This means that if your tsconfig.json file does not have
   a "files" property, and you add a new file to a directory
   configured by that tsconfig.json file, you will need to restart
   Sublime to get that file noticed.  The same applies to changes in
   the options properties of the tsconfig.json file.
4. Sublime Text 2 will be slow for files of about 2K lines or more.
   This happens because Sublime Text 2 does not reliably inform
   plug-ins of buffer changes and therefore the plug-in has to
   frequently send the entire view contents to the server.
5. By default, the plug-in retains the Sublime native behavior for
   auto indent (such as when typing the Enter key).  To have the
   TypeScript server supply auto indent, set the
   'typescript\_auto\_format' setting to true in your
   Preferences.sublime-settings file.  The plug-in does by default
   request TypeScript formatting upon typing ';' or '}'.  You can turn
   off TypeScript formatting on these characters by removing the key
   bindings from the Default.sublime-keymap file in the TypeScript
   package.
6. You can get TypeScript formatting for a line by typing 'ctrl+;'.
   You can get TypeScript formatting for a document by typing 'ctrl+t,
   ctrl+f'.  If a selection is present that same key sequence will
   format only the selection.  You can get TypeScript formatting for a
   block by typing 'ctrl+}' from within that block.  After formatting,
   the cursor will be placed outside the block, so that you can
   continue to type 'ctrl+}' to format the next outer block.
7. On Mac, the plug-in looks for the installed node executable on the
   default system path and also in the directory '/usr/local/bin'.  If your
   node installation placed the node executable elsewhere, then add
   the 'node\_path' setting to your Preferences.sublime-settings file.
   The value of the 'node\_path' setting should be the pathname of the
   node executable as in '/usr/myinstalldir/node'.  
   
