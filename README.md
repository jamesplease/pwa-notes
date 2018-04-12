# pwa-notes

> Last updated: 4/11/18

Progressive Web Apps are applications that are built with web technologies that
appear to the user to be native.

There are differences between native applications and web apps that are
important to keep in mind when making PWAs to help with the illusion
that the app is native.

These notes list some of those differences and things to be mindful of.

> Heads up! PWAs are a rapidly evolving technology. This information may be outdated
> if you are reading this many months or years after the last update.

## Environment

I am in an environment that is very bad for PWAs: Apple's operating systems.
This can be seen as a good thing; I am testing the worst-case scenario.

More specifically:

- **Desktop**:  macOS 10.13.4, Google Chrome Canary  
- **Mobile**: iOS 11.3.0, Safari

## Notes

### All /General

- Scrolling down when the page is at the top should not move the header. In
  iOS, this can be fixed by avoiding position:sticky and using position:fixed.
  However, macOS PWAs via Chrome always scroll the header, even with
  position:fixed. This may(?) be an OS-level thing, as Safari on macOS also
  scroll position:fixed.

  The Twitter PWA appears to disable scrolling on desktop OS's when the
  window's scrollTop is 0, which resolves the problem.
  
- Anything stuck to the bottom of the app, such as a nav, should also not
  scroll when the user scrolls to the very bottom.
  
- The landing page for the website should likely be different than landing
  page for a standalone app. Websites usually have an introductory
  landing page with a large call-to-action, such as signing up. Apps
  tend to either have an explore page (if the user is logged in or if
  there are no accounts) or a log in page.

- Hide the website footer. Websites usually have a footer with copyright
  information, and possibly some links. Footers are not usually an element
  of native apps.

- Consider implementing a different top-level navigation system. Websites
  tend to have menus in the header, iOS apps tend to have bottom menu
  bars, even at large resolutions (see: Apple Music, App Store, Etsy,
  Kickstarter)
 
 - Different OS should possibly have different layouts. Android/macOS/iOS.
  iOS app on macOS can look weird. Perhaps
  [platform.js](https://github.com/bestiejs/platform.js/) could help with this.

### macOS (via Chrome Canary)

- Consider enforcing the default cursor, even for links and buttons. Note
  that Slack does not do this, and it does not feel weird to me. Use
  your judgment!

### iOS (via Safari)

- The grey highlight on tap should be removed

- Most text in the UI should not be selectable

- Disable user scaling

## Problems / Limitations

These are unresolved problems or current limitations related to making a PWA
feel native.

### macOS

- Links display the URL in the "status bar" in Chrome. This is the link preview
  in the lower-left hand corner of the app. Although this feature is useful for
  the web, it does not feel native. There is currently no way to disable this.

- Apps cannot have a minimum width set. All PWAs can be resized to be 100px wide.

- An HTTP application will display the URL bar

## iOS

I learned about a number of the items on this list from this
[this excellent article](https://medium.com/@firt/progressive-web-apps-on-ios-are-here-d00430dee3a7)
on Medium by Maximiliano Firtman.

- Controlling the appearance of the status bar is limited

- Split View and Slide Over do not work

- There is no screenshot of the app in the task switcher

- PWAs frequently crash upon being opened (I was able to reproduce this behavior
  on Pokedex, Twitter, and three side projects). This is easiest to replicate
  by opening the app, returning to the home screen, opening the app, and so on,
  until it crashes.

- Discovery of PWAs is poor. The user must go to the share sheet and add
  it to the home screen.

- There is no way to lock the orientation of the PWA.

- There is most likely no support for splash screens (I need to test this further).

- PWAs do not keep state between sessions. Once the user navigates away,
  the app will be shut down and reloaded.

- There is no background processing in PWAs.

- There is no API for knowing when the keyboard is open, so strange scrolling
  situations can occur. To observe this, open the Twitter PWA and click the button
  to compose a new tweet. Then, scroll down.

## Things to Test

These are things that I still need to test on mobile and desktop.

- A user clicking an external webpage link from within a PWA. Does it load the
  webpage within the PWA, or does it open the browser? What about links that
  attempt to open in a new tab?

- Displaying a splash image on iOS
  ([reference](https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html))

## Useful Tips

- You can apply CSS to standalone apps using
  [media queries](https://gist.github.com/jamesplease/06a3c7da1ebf3c6e8d7b0ecc7e3a7a0d)

- You can also detect standalone mode
  [with JavaScript](https://stackoverflow.com/questions/21125337/how-to-detect-if-web-app-running-standalone-on-chrome-mobile?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa).