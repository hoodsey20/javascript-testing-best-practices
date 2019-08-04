## ⚪ ️ 3.5. Watch how the content is served over the network

:white_check_mark: **Do:** Apply some active monitor that ensure the page load under real network is optimized including any UX concern like slow page load or unminified bundle. It's advisable to have these rich monitors both during development and also 24x7 over the production's servers/CDN. The inspection tools market is no short: basic tools like pingdom, AWS cloudwatch, gcp StackDriver can be easily configured to watch whether the server is alive and response under a reasonable SLA. This only scratches the surface of what might get wrong: it's preferable to opt for tools that specializes in frontend (e.g. lighthouse, pagespeed) and perform richer analysis of symptoms like page load time, meaningful paint (i.e. content seems ready for the user), time until the page gets interactive (TTI) to causes like ensuring the content is compressed, the time to first byte (i.e. network issues), optimize images, ensuring reasonable DOM size, SSL and many others. 

<br/>

:negative_squared_cross_mark: **Otherwise:** It must be disappointing to realize that after such a great care for crafting an UI, 100% functional tests passing and and sophisiticated bundling - the UX is horrible and slow due to CDN misconfiguration

<br/>

### :clap: Doing It Right Example: Lighthouse page load inspection report

![](/assets/lighthouse2.png "Lighthouse page load inspection report")

<br/>