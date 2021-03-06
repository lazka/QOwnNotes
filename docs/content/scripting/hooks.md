# Hooks

onNoteStored
------------

!!! help "Method call and parameters"
    ```js
    /**
     * This function is called when a note gets stored to disk
     * You cannot modify stored notes, that would be a mess since
     * you are most likely editing them by hand at the same time
     *
     * @param {NoteApi} note - the note object of the stored note
     */
    function onNoteStored(note);
    ```

You may want to take a look at the example
[on-note-opened.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/on-note-opened.qml).

noteOpenedHook
--------------

!!! help "Method call and parameters"
    ```js
    /**
     * This function is called after a note was opened
     *
     * @param {NoteApi} note - the note object that was opened
     */
    function noteOpenedHook(note);
    ```

You may want to take a look at the example
[on-note-opened.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/on-note-opened.qml).

noteDoubleClickedHook
---------------------

!!! help "Method call and parameters"
    ```js
    /**
     * This function is called after a note was double clicked
     *
     * @param {NoteApi} note - the note object that was clicked
     */
    function noteDoubleClickedHook(note);
    ```

You may want to take a look at the example
[external-note-open.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/external-note-open.qml).

insertMediaHook
---------------

!!! help "Method call and parameters"
    ```js
    /**
     * This function is called when media file is inserted into the note
     * If this function is defined in multiple scripts, then the first script that returns a non-empty string wins
     *
     * @param fileName string the file path of the source media file before it was copied to the media folder
     * @param mediaMarkdownText string the markdown text of the media file, e.g. ![my-image](file://media/505671508.jpg)
     * @return string the new markdown text of the media file
     */
    function insertMediaHook(fileName, mediaMarkdownText);
    ```

You may want to take a look at the example
[example.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/example.qml).

insertingFromMimeDataHook
-------------------------

!!! help "Method call and parameters"
    ```js
    /**
     * This function is called when html or a media file is pasted to a note with `Ctrl + Shift + V`
     *
     * @param text text of the QMimeData object
     * @param html html of the QMimeData object
     * @returns the string that should be inserted instead of the text from the QMimeData object
     */
    function insertingFromMimeDataHook(text, html);
    ```

You may want to take a look at the example
[example.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/example.qml),
[insert-headline-with-link-from-github-url.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/insert-headline-with-link-from-github-url.qml)
or
[note-text-from-5pm-mail.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/note-text-from-5pm-mail.qml).

handleNoteTextFileNameHook
--------------------------

!!! help "Method call and parameters"
    ```js
    /**
     * This function is called when a note gets stored to disk if
     * "Allow note file name to be different from headline" is enabled
     * in the settings
     *
     * It allows you to modify the name of the note file
     * Keep in mind that you have to care about duplicate names yourself!
     *
     * Return an empty string if the file name of the note should
     * not be modified
     *
     * @param {NoteApi} note - the note object of the stored note
     * @return {string} the file name of the note
     */
    function handleNoteTextFileNameHook(note);
    ```

You may want to take a look at the example
[example.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/example.qml)
or
[use-tag-names-in-filename.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/use-tag-names-in-filename.qml).

handleNoteNameHook
------------------

!!! help "Method call and parameters"
    ```js
    /**
     * This function is called when the note name is determined for a note
     *
     * It allows you to modify the name of the note that is viewed
     *
     * Return an empty string if the name of the note should not be modified
     *
     * @param {NoteApi} note - the note object of the stored note
     * @return {string} the name of the note
     */
    function handleNoteNameHook(note);
    ```

You may want to take a look at the example
[example.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/example.qml).

It may not be a good idea to use this hook if the setting to use the
file name as note name is active.

handleNewNoteHeadlineHook
-------------------------

!!! help "Method call and parameters"
    ```js
    /**
     * This function is called before a note note is created
     *
     * It allows you to modify the headline of the note before it is created
     * Note that you have to take care about a unique note name, otherwise
     * the new note will not be created, it will just be found in the note list
     *
     * You can use this method for creating note templates
     *
     * @param headline text that would be used to create the headline
     * @return {string} the headline of the note
     */
    function handleNewNoteHeadlineHook(headline);
    ```

You may want to take a look at the example
[custom-new-note-headline.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/custom-new-note-headline.qml).

preNoteToMarkdownHtmlHook
-------------------------

!!! help "Method call and parameters"
    ```js
    /**
     * This function is called before the markdown html of a note is generated
     *
     * It allows you to modify what is passed to the markdown to html converter 
     *
     * The method can for example be used in multiple scripts to render code (like LaTeX math or mermaid)
     * to its graphical representation for the preview
     *
     * The note will not be changed in this process
     *
     * @param {NoteApi} note - the note object
     * @param {string} markdown - the markdown that is about to being converted to html
     * @return {string} the modified markdown or an empty string if nothing should be modified
     */
    function preNoteToMarkdownHtmlHook(note, markdown);
    ```

You may want to take a look at the example
[preview-styling.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/preview-styling.qml).

noteToMarkdownHtmlHook
----------------------

!!! help "Method call and parameters"
    ```js
    /**
     * This function is called when the markdown html of a note is generated
     *
     * It allows you to modify this html
     * This is for example called before by the note preview
     *
     * The method can be used in multiple scripts to modify the html of the preview
     *
     * @param {NoteApi} note - the note object
     * @param {string} html - the html that is about to being rendered
     * @return {string} the modified html or an empty string if nothing should be modified
     */
    function noteToMarkdownHtmlHook(note, html);
    ```

You may want to take a look at the example
[example.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/example.qml)
or
[preview-styling.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/preview-styling.qml).

Please refer to the [Supported HTML
Subset](http://doc.qt.io/qt-5/richtext-html-subset.html) documentation
for a list of all supported css styles.

encryptionHook
--------------

!!! help "Method call and parameters"
    ```js
    /**
     * This function is called when text has to be encrypted or decrypted
     *
     * @param text string the text to encrypt or decrypt
     * @param password string the password
     * @param decrypt bool if false encryption is demanded, if true decryption is demanded
     * @return the encrypted decrypted text
     */
    function encryptionHook(text, password, decrypt);
    ```

You may want to take a look at the example
[encryption-keybase.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/encryption-keybase.qml),
[encryption-pgp.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/encryption-pgp.qml)
or
[encryption-rot13.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/encryption-rot13.qml).

noteTaggingHook
---------------

You can implement your own note tagging mechanism for example with
special text in your note like `@tag1`, `@tag2`, `@tag3`.

!!! help "Method call and parameters"
    ```js
    /**
     * Handles note tagging for a note
     *
     * This function is called when tags are added to, removed from or renamed in
     * a note or the tags of a note should be listed
     *
     * @param note
     * @param action can be "add", "remove", "rename" or "list"
     * @param tagName tag name to be added, removed or renamed
     * @param newTagName tag name to be renamed to if action = "rename"
     * @return string or string-list (if action = "list")
     */
    function noteTaggingHook(note, action, tagName, newTagName);
    ```

-   as soon as a script is activated that implements the new function
    `noteTaggingHook` note tagging will be handled by that function
-   following features should work via the QOwnNotes user interface

    -   initially importing tags like `@tag` from your notes and
        overwriting your current tag assignment
        -   you will not loose your tags tree, just the former assignment
            to notes
        -   you can still move tags into other tags
        -   if more than one tag has the same name in your tag tree the
            first hit will be assigned
    -   adding a tag to a note will add the tag to the note text
    -   removing a tag from a note will remove the tag from the note text
    -   removing of tags in the tag list will remove those tags from your
        notes
    -   renaming of tags in the tag list will rename those tags in your
        notes
    -   bulk tagging of notes in the note list will add those tags to your
        notes
    -   bulk removing of tags from notes in the note list will remove
        those tags from your notes

You may want to take a look at the example
[note-tagging.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/note-tagging.qml)
to implement your own tagging mechanism.

autocompletionHook
------------------

You can return a list of strings to be added to the autocompletion list
when the autocompletion is invoked.

!!! help "Method call and parameters"
    ```js
    /**
     * Calls the autocompletionHook function for all script components
     * This function is called when autocompletion is invoked in a note
     *
     * @return QStringList of text for the autocomplete list
     */
    function callAutocompletionHook();
    ```

You may want to take a look at the example
[autocompletion.qml](https://github.com/pbek/QOwnNotes/blob/develop/doc/scripting/autocompletion.qml).
