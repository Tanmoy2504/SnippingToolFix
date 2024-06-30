# SnippingToolFix
Guide to fix the **‘Screenshot copied to clipboard, but couldn’t save’** error in Snipping Tool for Windows 10/11 <br><br>
Original Credit goes to MiniTool for documenting the fix [Here](https://www.minitool.com/data-recovery/windows-not-saving-screenshots-to-screenshots-folder.html#:~:text=Step%201.%20Press%20Windows%20%2B%20R%20key%20combination)<br><br>
<br>
> [!NOTE]
> I have created a registry file named **SnippingToolFix.reg** which can be downloaded and imported directly instead of manually tweaking registry. This will reset the directory location to default and incase the registry are missing, it will create the respective entries explained below. <br><br> **However users still need to create the folders in respective directories** or they can use the code inside command prompt to automate the same
<br>

> [!WARNING]
> This goes without saying that since we will be editing registry, it will be wise to make a ***registry backup or a full system backup*** incase of a mishap. _By proceeding forward, you are acknowledging the risks involved and that I shall not be held liable_ incase of damage caused to your system. <br><br>
> This event shouldn't occur unless user makes some mistake or change any setting which is not mentioned in this guide hence the strong recommendation for a backup

### The Problem: <br><br>
The error occurs when the “Screenshots” folder inside the “Pictures” folder is missing or if the user uninstalls OneDrive.
The Windows registry points to an invalid location, triggering the issue.
<br><br>
### The Solution:<br><br>
Navigate to “HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer”
<br>

Create a DWORD (32 Bit) Value  named **Screenshotindex** vith value 1 (in Hexadecimal mode) <br><br>

Now navigate to “HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders.”
<br>
Correct these two registry entries: <br><br>

>{B7BEDE81-DF94-4682-A7D8-57A52620B86F}  ->  (points to the Screenshots folder location)

>{EDC0FE71-98D8-4F4A-B920-C8DC133CB165}  ->  (points to the snipping tool's screen record folder location)<br>
<br>

Edit the data in the entries so that the folowing keys have the following values: <br><br>
{B7BEDE81-DF94-4682-A7D8-57A52620B86F}   ->  %USERPROFILE%\Pictures\Screenshots

{EDC0FE71-98D8-4F4A-B920-C8DC133CB165}   ->  %USERPROFILE%\Videos\Captures
<br><br>

>[!TIP]
>**It is best to use %USERPROFILE% for reliability instead of hardcoding the folder location unless the user wants to point to different location other than default.**
<br><br>

Create folders named “Screenshots” and “Captures” in their respective locations.<br><br>
Alternatively you can just run the following command in command prompt to make the job easier <br><br>
```
mkdir %USERPROFILE%\Pictures\Screenshots && mkdir %USERPROFILE%\Videos\Captures
```
<br>

> [!WARNING]
>**The app expects the folder "Screenshots" and "Captures" to exist; Snipping tool app won’t create it automatically. Users must manually create the folder or use the command above, else the errors will persist.**
<br><br>

Close the Snipping Tool and restart explorer.exe from the taskbar or give it a full restart whichever is convinient
<br><br>

> [!IMPORTANT]
> If the registry entries **{B7BEDE81-DF94-4682-A7D8-57A52620B86F}** and **{EDC0FE71-98D8-4F4A-B920-C8DC133CB165}** don’t exist, right-click on “New > Expandable String Value” which will create a key with type **REG_EXPAND_SZ**. Now create the entries, ensuring the curly brackets are included or use the registry file to avoid the hassle <br>
- [x] {B7BEDE81-DF94-4682-A7D8-57A52620B86F} registry key name is valid
- [x] {EDC0FE71-98D8-4F4A-B920-C8DC133CB165} registry key name is valid
- [ ] B7BEDE81-DF94-4682-A7D8-57A52620B86F is invalid
- [ ] EDC0FE71-98D8-4F4A-B920-C8DC133CB165 is invalid
