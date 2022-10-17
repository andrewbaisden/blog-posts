## CSS and JavaScript accessibility best practices

[CSS and JavaScript accessibility best practices - Learn web development | MDN](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/CSS_and_JavaScript)

[An introduction to Web Accessibility - YouTube](https://www.youtube.com/watch?v=9I-DCEa1WhM)

[Web Fundamentals | Google Developers](https://developers.google.com/web/fundamentals/)

[The A11Y Project](https://a11yproject.com/)

- Using rems/ems instead of px so that the font scales in a uniform way for the webpage or app. So if the user was to change the font size for their browser to something smaller or bigger. All of the font on the website would scale in proportion. So it is very good for accessibility and people who have vision problems. The same applies to everything in the box model too like margin and padding.
- Using developer browser tools like google lighthouse and Accessibility Developer Tools, to audit for performance, accessibility, progressive web apps, and more
- Using buttons for performing actions and anchor tags for leading somewhere
- Using aria-label for buttons with icons as it allows screen readers to give an audio representation of what the button is. As people with disabilities might not be able to see the button clearly or at all
- Using flex box or css grid for tab order. Because if you use floats it breaks the positioning for tab order and keyboard accessibility which works from left to right. Or right to left if you are using a language like Arabic.
- Having an appropriate focused outline colour for focused html elements on a web page. The default colour is blue so if you have a blue button, you could change it to red. Or you could change it to another colour depending on the brand style of your website.

## Device and Browser Testing

### Apple Ecosystem

**Macbook**
Use the built in Simulator App for simulating iOS devices

Use system preferences > display to scale the display resolution up and down

**Lighthouse**
[Lighthouse | Tools for Web Developers | Google Developers](https://developers.google.com/web/tools/lighthouse/)

Make sure that its installed first

```bash
npm install -g lighthouse
# or use yarn:
# yarn global add lighthouse
```

Using the Node CLI

```bash
lighthouse --view https://www.google.com/
```

Replace the website address with whatever website you want to test

**Mobile Phones**
Use for testing apps running native

**Web Browsers**
Use the Inspect Element

Use browser developer tools (React and Vue)

Use Responsive Design mode and the CSS Grid Layout Inspector in Firefox

### Windows, Android and Linux

[Cross Browser Testing Tool. 1000+ Browsers, Mobile, Real IE.](https://www.browserstack.com/#)

https://saucelabs.com/

[Cross Browser Testing Tool: 1500+ Real Browsers & Devices](https://crossbrowsertesting.com/)

## Bug and error tracking

[LogRocket | Logging and Session Replay for JavaScript Apps](https://logrocket.com)

[Sentry | Error Tracking Software — JavaScript, Python, PHP, Ruby, more](https://sentry.io/welcome/)

[Error Tracking & Crash Reporting for Software Developers - Rollbar](https://rollbar.com)

## SEO Tools

Google Analytics

[Google Webmasters – Support, Learn, Connect & Search Console – Google](https://www.google.com/webmasters/#?modal_active=none)

[web.dev | web.dev](https://web.dev/)

[Bing - Webmaster Tools](https://www.bing.com/toolbox/webmaster)

https://www.hotjar.com

## Useful Links

[Search Engine Optimization (SEO) Starter Guide - Search Console Help](https://support.google.com/webmasters/answer/7451184?hl=en)

[How to set up your website & monitor its search traffic in Google Search Console | 9to5Google](https://9to5google.com/2018/01/30/how-to-setup-and-optimze-for-google-search-console/?pushup=1)

[Create your Google Sitemap Online - XML Sitemaps Generator](https://www.xml-sitemaps.com/)

[Online Sitemap Generator • XML • HTML • RSS • Google](https://xmlsitemapgenerator.org/sitemap-generator.aspx)

**SEO optimisation ideas**
https://en-gb.wordpress.org/plugins/all-in-one-seo-pack/

[Yoast SEO: the #1 WordPress SEO Plugin • Yoast](https://yoast.com/wordpress/plugins/seo/)
