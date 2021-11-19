---
layout:     post
author:     Juande Santander-Vela
title:     "Re-enabling the prompt to open a particular application from a URL in Safari, Firefox, and Chrome"
categories: Miro Chrome Firefox "application pop-up" macOS
---

> This is a partial post; I prefer to post it in progress, as I think it can help some people even if it is not finished. Polish will come later…

At SKAO we use [Miro][1] for many, many things: from sprint retrospectives, to roadmaps, to brainstormings… we do have many uses for Miro.

However, Miro is quite resource intensive, and we have found that using the [Miro Desktop Application][2] requires much less CPU than using it in the browser. So, at some point, I decided to check the *Don't ask again checkbox*, and be done with it.

However, I normally prefer to show only my browser window through Zoom, and then it becomes handy not to have Miro boards open automatically in the app, but wait for the 

I'm currently beta-testing a Chrome-based browser of which I cannot say more, and I could not find a way to restore the prompt. However, thanks to [this Miro FAQ][3], I found is the answer, as apart from telling you how to remove the pop-up, it also shows you how to revert it.

## For Chrome (and other Blink-based browsers)

1. Close all Chrome + Miro windows before starting (use Cmd + Q to quit the browser).
1. Open Finder on your Mac > press Command + Shift + G > enter the following path into the search box: `~/Library/Application Support/Google/Chrome`. Open your Chrome profile folder, and find the `Preferences` file.
1. There may be several folders with the file, please try the next suggestions:
    1. open and search for the `Preferences` file inside the `Default` folder, if you have just one profile in Google Chrome; or
    1. open and search the `Preferences` file inside a `Profile X` folder if you have several profiles in Google Chrome, where `X`  is a number from the profile list.
    1. open and search `Preferences` inside each folder (`Default`, `Guest Profile`, `Profile X`), if they exist
1. Open Preferences in a text editor.
1. Search for` https://miro.com":{"miroapp":true}`.
1. Remove `https://miro.com":{"miroapp":true}`.
1. Save changes.
1. Restart Chrome browser.

If you use several Google profiles, you will need to edit the `Preferences` file in all of them catalogs. For this, on step 2, you will need to open `~/Library/Application Support/Google/Chrome` and change the `Preferences` file in folders `Profile 1`, `Profile 2`, etc.

The instructions above are also valid for Microsoft Edge, changing `Google/Chrome` for `Microsoft\ Edge`; for Brave, changing `Google/Chrome` for `BraveSoftware`… and you can try to identify other mappings for other browsers. But the end result is that the Preferences file is a JSON file, and you need to remove the entry about Miro.

## For Firefox
1. Open browser settings.
1. In the General section scroll down to Applications.
1. Find miroapp and change Use Miro (default) to Always ask by selecting the option in the drop-down menu.


If you are not using macOS, you can go to the aforementioned [Miro Help Page][3], and look for Windows instructions. 

Bear in mind that this is not specific to Miro: if you search for XXXXXX, this is also true, say, for a `tel:` link opening in FaceTime of Skype, for instance. You just have to search for YYYYYY, and remove the relevant elements in the JSON file.

[1]: https://miro.com "Miro: Online Whiteboard"
[2]: https://miro.com/apps/ "Miro: Download Miro Apps"
[3]: https://help.miro.com/hc/en-us/articles/360019244239-How-to-disable-Miro-Desktop-app-pop-up-in-your-browser "Miro Help Center: How to disable Miro Desktop app pop-up in your browser"