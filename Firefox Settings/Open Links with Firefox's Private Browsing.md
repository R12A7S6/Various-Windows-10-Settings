Open links with Firefox's Private Browsing:

Foreword:
Allows all links clicked outside of a web browser (ie. Desktop Shortcut, Windows' Mail app) to be opened with a new or existing Firefox's Private Window.
Somewhat niche, but this is useful when the "Always use private browsing mode" option is too extreme in that it disables certain desirable functions of the regular browsing mode. In particular, the regular browsing mode allows the container tabs to be used, preserved tabs to be reopened and important visited sites to be saved (delegating unimportant sites to the private window).


Option 1:
https://support.mozilla.org/en-US/questions/1242740#answer-1178923

---

jscher2000 - Support Volunteer
jscher2000 - Support Volunteer

    Top 10 Contributor

12/6/18, 12:14 PM
Chosen Solution

Hi Kish_B, Outlook's right-click context menu for links doesn't let you choose a specific program, so I think you have two possible workarounds:

(1) Find a launcher program to stand in as your default browser and let you decide, on a link-by-link basis, where you want to send it.

(2) Edit the URL handler setting in the Windows registry.

If you want to try that (and you promise not to mess things up in there!), here's how:

(A) Start the RegEdit.exe program (if you type regedit in the Windows Start menu search box, a link to the program will come up among the results)

(B) In the left pane, expand:

HKEY_CLASSES_ROOT

=> FirefoxURL*

=> shell

=> open

=> command

* Note: There may be additional FirefoxURL entries, as noted in the attached "Before" screenshot, if you made simultaneous installations of Firefox. You'll want to modify the one that matches up with your current main installation.

(C) On the right side, the (Default) value will be either of these (depending on the program installation folder):

    "C:\Program Files\Mozilla Firefox\firefox.exe" -osint -url "%1"
    "C:\Program Files (x86)\Mozilla Firefox\firefox.exe" -osint -url "%1" 

That instructs Windows to call Firefox and passes the URL to it ("%1" is replaced by the URL).

Found it? Now you will edit the command and replace

-url

with

-private-window

So you will end up with one of these:

    "C:\Program Files\Mozilla Firefox\firefox.exe" -osint -private-window "%1"
    "C:\Program Files (x86)\Mozilla Firefox\firefox.exe" -osint -private-window "%1" 

The "After" screenshot is attached.

(D) Test -- before closing RegEdit, try a lik in Outlook and it should open in a private window instead of a regular window.

Success?

It's possible that your next Firefox update, or triggering Firefox to make itself the default browser, will switch this back to its default value, so be on the lookout for that.

---

There are also FirefoxPDF-* and FirefoxHTML-* under HKEY_CLASSES_ROOT, which I assume are for opening PDF and HTML files with Firefox. The same procedures should be repeated for them if it is desirable to open them with Private Window.

Option 2:

1. Run CMD as Administrator.
2. Type "ftype" without the quotes and press Enter.
3a. Look for the line: FirefoxURL-* (where * denotes a string of digits and letters (actually hex value here)).
3b. Alternatively, copy the entire output with a mouse drag from its top to bottom, and paste into a Text Editor such as Notepad++, then Find (Ctrl+F) the string "FirefoxURL".
4. In the same CMD window, type in "ftype" followed by a space, then type in the entire line that you have found from Step 3a or 3b, but do NOT hit Enter yet. (For example, "ftype FirefoxURL-1234567890ABCDEF="C:\Program Files\Mozilla Firefox\firefox.exe" -osint -url "%1") (Tip: It helps to use Ctrl+C and Ctrl+V)
5. Replace "-url" with "-private-window". (Example: ftype FirefoxURL-1234567890ABCDEF="C:\Program Files\Mozilla Firefox\firefox.exe" -osint -private-window "%1")
6. Press Enter, then test with a link from Mail or Desktop to ensure it works. Otherwise, revert the change by first pressing the Up Arrow once on your keyboard in the CMD window, CMD will show your last input, then replace "-private-window" back to "url" (as seen from Step 4).
7 (Optional). Do the same with the lines FirefoxPDF-* and FirefoxHTML-* if you wish to open PDF and HTML files with a Firefox's Private Browsing window.