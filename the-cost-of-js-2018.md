# The Cost Of JavaScript In 2018
> By Addy Osmany on 01/08/2018

If client-side JavaScript isn’t benefiting the user-experience, ask yourself if it’s really necessary. Maybe server-side-rendered HTML would actually be faster. Consider limiting the use of client-side frameworks to pages that absolutely require them. Server-rendering and client-rendering are a disaster if done poorly.

## 📖The web is bloated by use "experience"

- Javascript is the most expensive part of your site.
- Measure.

### 📙Action Items 📙
- 💡 Apply code splitting and tree shaking.


## 📖The Film strip analogy

Three moments
  - Is it happenning?
    Transfering started.
  - Is it useful?
    Someone of value is seen in the page.
  - Is it usable?
    Interactive and fully engageable.
    
    Make the application interactive as fast as possible is one of the key things to get faster interactiion time.  
    TTI varies a lot depending on the devices. A good metrics suggested is under 5 seconds with (3G on a median mobile device)  
    Problem stated: Loading too much JavaScript into the main thread (via <script>, etc) is the issue. 

### 📙Action Items 📙
   
   💡 Pulling JS into a Web Worker or caching via a Service Worker doesn’t have the same negative Time-to-Interactive impact.
  
## 📖Why is Javascript so expensive
 There are a lot of things the browser request to start painting the page.(Not very detailed explanation here)
 
 - Parse and compile takes up to 30% of the time engine.
 - All bytes are not equal: 200kb js !== 200kb jpg

## 📖Mobile is a spectrum

> "stop taking fast networks and fast devices for granted"
- When variance can kill the user experience, developing with a slow baseline ensures everyone
 
 💡 Minify your code
 💡 Compress
 💡 Ship less
 💡 Take advantage of caching for repeat visits
 
## 📖Audit JS regularly

- [Webpack bundle analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer)
- [Source map explorer](https://www.npmjs.com/package/source-map-explorer)
- [Bundle buddy](https://github.com/samccone/bundle-buddy)

Look for lighter alternatives on libraries. e.g. date-fns instead of moment.

- [Libs optimizations from google](https://github.com/GoogleChromeLabs/webpack-libs-optimizations)

- [Lighthouse](https://developers.google.com/web/tools/lighthouse/)

## 📖Remove  unused code from the critical path

 💡 Use the codecoverage tool from chrome dev tools.

## 📖Perfomance budget in place

## 📖Performance and business
  - Create a performance vision.
  - Setup your budget.
    [lighthoust-ci](https://github.com/ebidel/lighthouse-ci)
  - Create regular report on KPI.
    [Webdash](https://github.com/jadjoubran/webdash)
 
## 📖Real user monitor
  - Long tasks.
  - [First input delay](https://developers.google.com/web/updates/2018/05/first-input-delay).


## Next
- [Can you afford it? Real world web perfomance budge](https://infrequently.org/2017/10/can-you-afford-it-real-world-web-performance-budgets/)
- [Smaller lodash bundles with webpack and babel](https://nolanlawson.com/2018/03/20/smaller-lodash-bundles-with-webpack-and-babel/)
- [State of Javascript](https://beta.httparchive.org/reports/state-of-javascript#bytesJs)
- [Tree shaking](https://developers.google.com/web/fundamentals/performance/optimizing-javascript/tree-shaking/)
- [A pinteres progressive web app](https://medium.com/dev-channel/a-pinterest-progressive-web-app-performance-case-study-3bd6ed2e6154)
- [PRPL pattern](https://developers.google.com/web/fundamentals/performance/prpl-pattern/)
