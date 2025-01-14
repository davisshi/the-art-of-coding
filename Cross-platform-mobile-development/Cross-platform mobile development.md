[The Pragmatic Engineer](https://newsletter.pragmaticengineer.com/)
===================================================================

Upgrade to paid

[Deepdives](https://newsletter.pragmaticengineer.com/s/deepdives/?utm_source=substack&utm_medium=menu)

[Cross-platform mobile development](https://newsletter.pragmaticengineer.com/p/cross-platform-mobile-development?utm_source=post-email-title&publication_id=458709&post_id=154832517&utm_campaign=email-post-title&isFreemail=true&r=w8lej&triedRedirect=true&utm_medium=email)
=================================

### A deep dive into the most popular frameworks: React Native, Flutter, native-first, and web-based technologies, and how to pick the right approach

[![](https://substackcdn.com/image/fetch/w_36,h_36,c_fill,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F802a32bb-2048-428b-bdb5-d6acd1e2b2d5_48x48.png)](https://substack.com/@pragmaticengineer)

[![](https://substackcdn.com/image/fetch/w_36,h_36,c_fill,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1f8831f0-97b4-4369-97a0-3ebc98f498d2_1298x1298.jpeg)](https://substack.com/@hejelin)

[![](https://substackcdn.com/image/fetch/w_36,h_36,c_fill,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7d9c17ab-c13d-4678-9d1c-a8be64009518_906x872.jpeg)](https://substack.com/@fatosmorina)

[Gergely Orosz](https://substack.com/@pragmaticengineer)

[Elin Nilsson](https://substack.com/@hejelin)

[Fatos Morina](https://substack.com/@fatosmorina)

Jan 14, 2025

114

[4](https://newsletter.pragmaticengineer.com/p/cross-platform-mobile-development/comments)

6 Share

These days, it seems almost everyone owns a smartphone. In the US, [91% of adults](https://www.pewresearch.org/internet/fact-sheet/mobile/) have one, in Europe, this figure is [89%](https://www.statista.com/forecasts/1147144/smartphone-penetration-forecast-in-europe), while in India, Deloitte [predicts](https://economictimes.indiatimes.com/industry/cons-products/electronics/india-to-have-1-billion-smartphone-users-by-2026-deloitte/articleshow/89750324.cms) 75% of adults will have a smartphone by 2026. In total, there are an [estimated 4.8 billion](https://www.bankmycell.com/blog/how-many-phones-are-in-the-world) smartphone users in the world, which is an incredible number! This means that for tech startups and tech businesses that build consumer products, it's a baseline expectation for them to be usable on smartphones, and for there to be a mobile app for the product.

So, how do you build mobile apps? There's plenty of choice: you can build a native mobile app for iOS using Swift or Objective C as a programming language, make one for Android using Java or Kotlin, and of course, you can develop a web app for desktop and mobile web users. All this adds up to three separate codebases and plenty of business logic replication.

Or you can do what startups like social media newcomer Bluesky did: have one codebase that powers the web, native iOS, and native Android apps. For Bluesky, a single developer wrote the initial version of all three apps using React Native and Expo. *We cover more on this in the article, [Inside Bluesky's engineering culture](https://newsletter.pragmaticengineer.com/i/145059916/mobile-and-web-stack).*

There are cross-platform frameworks and approaches that offer a way to use a single codebase to power multiple native apps and a website. A decade ago, most cross-platform technologies were in their early stages, but things are shifting; in October 2022, we covered whether more cross-platform development could lead to less [native iOS and Android hiring by startups](https://newsletter.pragmaticengineer.com/p/native-vs-cross-platform).

Today's article looks into current cross-platform development approaches, covering:

1.  **The ecosystem**. Most apps remain fully native, with Flutter and React Native (RN) the clear leaders for cross-platform development. RN is more popular in the US and UK, and apps built with it tend to generate more money.

2.  **React Native.** The framework of choice for many Meta, Microsoft, Amazon, and Shopify apps, and at places whose web teams work with React.

3.  **Flutter**. Built and championed by Google, and the framework for most cross-platform apps.

4.  **Native-first approaches.** Kotlin multiplatform, Swift-based frameworks (Skip, Scade), .NET MAUI (C#), NativeScript (JavaScript), and Unity.

5.  **Web-based frameworks**. Cordova, Capacitor, Ionic, and Progressive Web Apps.

6.  **Choosing the right framework**. A mental model for identifying key differences between all these technologies. *In the end, most teams choose React Native or Flutter.*

*The bottom of this article could be cut off in some email clients. [Read the full article uninterrupted, online.](https://newsletter.pragmaticengineer.com/p/cross-platform-mobile-development)*

[Read the full article online](https://newsletter.pragmaticengineer.com/p/cross-platform-mobile-development)

1\. The ecosystem
-----------------

What are the most popular cross-platform frameworks? Interesting [research by Appfigures](https://appfigures.com/resources/insights/20241025?f=1) looked at all the top apps on the iOS App Store and Android's Google Play, peeked into their binaries, and categorized them by the framework used:

[![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff8874ee7-f6c6-4837-8160-7ecf949ab82b_1560x962.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff8874ee7-f6c6-4837-8160-7ecf949ab82b_1560x962.png)

*The most popular frameworks for iOS and Android apps. Source: [Appfigures](https://appfigures.com/resources/insights/20241025?f=1)*

Other research published [on Statista](https://www.statista.com/statistics/869224/worldwide-software-developer-working-hours/) suggests Flutter and React Native are the most popular choices, followed by Cordova, Unity, and Ionic:

[![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1cc9d1ab-81e3-4539-9c86-91214eca2f5a_1422x908.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1cc9d1ab-81e3-4539-9c86-91214eca2f5a_1422x908.png)

*Cross-platform mobile adoption trends (2020-2023) based on a survey of 30,000 respondents. Flutter was used by 46% of respondents, and RN by 35% in 2023. Data source: [Statista](https://www.statista.com/statistics/869224/worldwide-software-developer-working-hours/)*

**Leaders: Flutter and React Native. **These are the two most popular frameworks, but it can be tricky to identify which one is the most popular: on iOS, there are more React Native-powered, and on Android, Flutter apps outnumber React Native ones. However, there are simply more Android apps than iOS ones, which is why there are more Flutter apps than React Native ones, overall. React Native has been around since 2015, and Flutter since 2017.

**Shrinking: Cordova and Ionic. **As per the Statista survey, both frameworks have smaller but shrinking market shares, with about 10-12% of survey participants using them. Their usage is likely more common at companies which were building cross-platform apps before React Native and Flutter emerged, and remain content to ship WebView-based applications.

**Growth potential: Kotlin Multiplatform (KMP).** This technology has modest adoption rates, but seems to be gaining momentum. JetBrains is investing heavily in it, while the Kotlin language is popular with native mobile developers, especially with Android folks.

#### React Native or Flutter more popular?

New data from the [2024 Stack Overflow Developer Survey](https://survey.stackoverflow.co/2024/) offers pointers. Below is a breakdown of the mobile cross-platform frameworks used by circa 6,500 respondents:

[

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F22c93702-59d5-46d6-a1a6-0cca0062eb61_1136x886.png)

](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F22c93702-59d5-46d6-a1a6-0cca0062eb61_1136x886.png)

*Cross-platform mobile framework usage by developers. Data source: [Stack Overflow](https://survey.stackoverflow.co/2024/)*

From this data, it's clear that Flutter and React Native are the most popular by a distance, with more users than all other frameworks, combined. But which is the most popular, overall? To find out, let's slice and dice the data; firstly by narrowing it down to only professional developers by removing hobbyist users:

[

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe4d58f32-c39b-4f38-81f3-1f37e0854d8c_1080x444.png)

](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe4d58f32-c39b-4f38-81f3-1f37e0854d8c_1080x444.png)

*Framework usage by professional developers of cross-platform apps. Source: [Stack Overflow Developer Survey](https://survey.stackoverflow.co/2024/)*

Flutter is used by slightly more engineers, though the difference is perhaps smaller than before. What happens if we consider per-country usage? Let's start with the US, UK, Canada and Australia:

[

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fee8bb377-5652-457b-bbb1-9280a17f936a_1600x697.png)

](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fee8bb377-5652-457b-bbb1-9280a17f936a_1600x697.png)

*Flutter vs React Native usage by country. Source: [Stack Overflow Developer Survey](https://survey.stackoverflow.co/2024/)*

Let's look at other countries with a higher number of responses -- the Netherlands, France, Poland, Brazil, Germany, and India:

[

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc8699b88-399d-456f-a405-69f0de52848a_1698x1048.png)

](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc8699b88-399d-456f-a405-69f0de52848a_1698x1048.png)

*Flutter vs React Native usage by country. Source: [Stack Overflow Developer Survey](https://survey.stackoverflow.co/2024/)*

**Developer framework preference seems to be linked to location. **Germany and India somewhat prefer Flutter, while the US and UK tend towards React Native. I don't have an explanation of the difference in preference by country; specifically: why Flutter is so much more favored in Germany, but React Native more popular in the US and UK. If you have any thoughts on this, please share in the comment section, below.

[Leave a comment](https://newsletter.pragmaticengineer.com/p/cross-platform-mobile-development/comments)

**Flutter powers more apps, but React Native ones earn more revenue.** It's hard to accurately measure developers' preferences, but determining the number of apps using each framework is easier. Appfigures did exactly this by tracking all apps released in a year and found that Flutter was used by 11% of apps released in 2024, while 7% used React Native:

[

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe6bcc5db-b7f7-4132-928e-1a3df467378b_1596x966.png)

](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe6bcc5db-b7f7-4132-928e-1a3df467378b_1596x966.png)

*Around 11% of apps released in 2024 used Flutter, 7% used React Native, and 4% Unity. Source: [Appfigures](https://appfigures.com/resources/insights/20241025?f=1)*

Appfigures also [estimates](https://appfigures.com/resources/insights/20241025?f=1) revenue generated by apps. Despite having fewer users, React Native-built apps on aggregate generated more net revenue ($287M) than Flutter apps ($283M), after Apple and Google's 30% cuts.

The following section looks into each framework.

2\. React Native
----------------

React Native appears to be the most popular cross-platform framework in the US and UK markets. What are the likely reasons for this popularity?

-   **No need for frontend developers to learn a new language. **Developers who know JavaScript or TypeScript will have no trouble getting started with React Native, and devs working with React will find the transition especially easy. As we know, React is the most popular frontend framework, with around 70% of frontend developers using it in 2024, as per the [State of Frontend 2024](https://tsh.io/state-of-frontend/#frameworks) survey.

-   **Easy enough to hire for.** React's popularity means it's a bit easier to hire for this skillset, than for native iOS or Android developers. The challenge of hiring native developers was one reason Coinbase [moved](https://www.coinbase.com/en-nl/blog/announcing-coinbases-successful-transition-to-react-native) to React Native in 2021.

-   **Expo. **The [Expo framework](https://expo.dev/) is built to simplify development with React Native, and is especially useful for teams. It helped boost adoption of React Native; without Expo, developers must set up both Android Studio and Xcode, manage emulators and simulators, and manage the native code. React Native's own documentation [recommends](https://reactnative.dev/docs/environment-setup) using Expo when getting started, as doing so without it makes the work [several times more complex](https://reactnative.dev/docs/getting-started-without-a-framework). Most of Expo is open source, but some services like Expo Application Services (EAS) have paid tiers.

React Native was open sourced by Facebook, in 2015. As the name suggests, this framework allows creating cross-platform apps using syntax similar to React applications. Here's how a "Hello, World" app looks like using React Native:

[![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdf1a4f0e-03a2-481d-bf48-111410ea4246_1600x1200.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdf1a4f0e-03a2-481d-bf48-111410ea4246_1600x1200.png)

*A simple React Native example. Source: [React Native documentation](https://reactnative.dev/docs/tutorial)*

React primitives render to native platform UI elements, which means the compiled app uses the same native UI elements as native iOS and Android apps.

*Check out a [behind-the-scenes peek into how the React.js documentary was created](http://react.js/) from two years ago.*

#### Well-known React Native apps

Some popular apps built with this technology include:

**Discord. **The social platform [moved](https://discord.com/blog/why-discord-is-sticking-with-react-native) to React Native in 2016 for iOS, and in 2018, two engineers rebuilt the iOS app in React Native at a time when the app already had millions of daily users. The team held off on moving to Android for performance reasons, until in 2022 they [moved](https://discord.com/blog/android-react-native-framework-update) the Android app to React Native; sharing the same codebase, and keeping iOS and Android-specific UI for each platform.

It's worth noting Discord often opts for cross-platform technologies: its desktop apps for Windows, Mac, and Linux are based on [Electron](https://www.electronjs.org/); a cross-platform desktop technology based on JavaScript, HTML, and CSS.

[![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc6fa2d7d-7a70-4d47-9a20-bfeb853b50f3_1600x750.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc6fa2d7d-7a70-4d47-9a20-bfeb853b50f3_1600x750.png)

Discord's iOS and Android app. Source: Discord

**Coinbase** moved to React Native [in 2021](https://www.coinbase.com/en-nl/blog/announcing-coinbases-successful-transition-to-react-native), when it had 56 million users and $1.8B in revenue. Moving off native to RN involved migrating more than 200 screens, and retraining more than 30 native-only engineers. Interestingly, Coinbase [claimed](https://www.coinbase.com/en-nl/blog/announcing-coinbases-successful-transition-to-react-native) that moving to RN reduced their cold start time from 3.8 seconds to 2.5 seconds (still quite a lot, to be fair!), and improved reliablity by increasing the crash-free rate from 99.4% to 99.7%.

A big motivation seemed to be to build more with fewer engineers, and make more consistent app experiences across platforms. The company labelled the transition a success: it reduced the number of codebases from 3 (iOS, Android and Web) to 2 (React Native and React Web), and web engineers could work on the mobile app, and mobile engineers on the web one.

[![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F20d4ae54-c0d6-4f93-a32c-0bdfe6b2963b_1400x799.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F20d4ae54-c0d6-4f93-a32c-0bdfe6b2963b_1400x799.png)

*Coinbase app built using React Native. Source: [Coinbase](https://www.coinbase.com/en-nl/blog/announcing-coinbases-successful-transition-to-react-native)*

**Shopify **went all-in on React Native five years ago. Just this week, the company reflected on how it went, [sharing](https://shopify.engineering/five-years-of-react-native-at-shopify?q=v):

-   **More productivity:** thanks to one codebase powering iOS and Android, and working across both apps

-   **Performance and reliability: **all pages have sub-500ms loads and crash-free rates are above 99.9%. Both are impressive numbers!

-   **TypeScript for the win**: using TypeScript makes it easy for devs to transfer between React and React Native.

-   **There are downsides:** debugging is worse than for native apps, and updating to new React Native versions can be painful.

Shopify employs more than 2,000 software engineers, and is one of the largest tech companies to go *all-in* on this technology. That it's working for them, five years later, is a strong vote of confidence. *Read more about [Shopify's 5-year reflections on RN](https://shopify.engineering/five-years-of-react-native-at-shopify?q=v).*

**Meta, Microsoft, and Amazon** are not known for fully React-native apps, but do use plenty of RN functionality in their apps:

-   **Meta**: React Native's creator utilizes it heavily for Facebook, Instagram, Ads Manager, Messenger, and Meta Horizon. The company recently [shared](https://engineering.fb.com/2024/10/02/android/react-at-meta-connect-2024/) that more than of its 5,000 engineers work with React code, and Meta apps have some clever React Native-related performance enhancements; for example, in the Facebook app, React Native is initialized when a user visits the first React Native surface, and not on app start. This allows for faster app startup.

-   **Microsoft**: the tech giant uses both React and React Native in products like Windows, XBox, Microsoft Office, Microsoft Teams, and other apps. The Windows maker is a heavy user of this technology for native performance and cross-platform code sharing reasons, as it [said](https://devblogs.microsoft.com/react-native/2022-09-02-rneu-microsoft-billions/) in 2022. Microsoft has also started to invest heavily in [React Native for Windows and MacOS](https://microsoft.github.io/react-native-windows/).

-   **Amazon**: parts of Amazon Shopping, Amazon Alexa, and Amazon Photos also utilize RN, as per the React Native showcase. Also, Amazon's Kindle device uses it.

The home screen of Kindle is rendered with React Native, after Amazon migrated away from a Java-based UI [in 2022](https://goodereader.com/blog/electronic-readers/amazon-kindle-ui-is-switching-from-javascript-to-react-native).

[![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fea81123e-7ef0-49aa-b123-d94e16a94900_1280x720.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fea81123e-7ef0-49aa-b123-d94e16a94900_1280x720.png)

*The Kindle home screen is rendered using React Native. Source: [Goodreader](https://goodereader.com/blog/electronic-readers/amazon-kindle-ui-is-switching-from-javascript-to-react-native)*

There are plenty of other, well-known apps building on top of React Native. Bloomberg [moved over](https://www.bloomberg.com/company/stories/bloomberg-used-react-native-develop-new-consumer-app/) to this framework shortly after it was launched, back in 2016.

[![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F92ede853-0298-40a7-a673-b362d0b11568_1600x718.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F92ede853-0298-40a7-a673-b362d0b11568_1600x718.png)

*Some high-profile apps that use React Native, even if not built exclusively with it. Source: [React Native showcase](https://reactnative.dev/showcase)*

3\. Flutter
-----------

[Flutter](https://flutter.dev/) was launched in 2017 by Google as a solution for cross-platform development. Initially, it targeted Android developers, allowing them to write code once for separate Android and iOS native applications.

Flutter uses the Dart programming language, a strongly-typed language with similar syntax to C# and Java. A clear downside of Flutter is the requirement to learn Dart. However, this is easy to pick up, especially with experience of Java or Kotlin. Here's what a simple Flutter application looks like:

[![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F080ae2dc-e62c-4256-9ea3-ae4af6fb3b7f_1230x1414.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F080ae2dc-e62c-4256-9ea3-ae4af6fb3b7f_1230x1414.png)

A simple Flutter app, written in Dart

RN uses native elements, but Flutter uses its own rendering engine called the [Impeller rendering engine](https://docs.flutter.dev/perf/impeller). This design choice means Flutter offers consistent UI experience across iOS and Android -- and even the web! The rendering engine and the programming language of choice are the biggest differences compared to React Native, and native development. Here is how [Jordan Bonnet](https://www.linkedin.com/in/jordanbonnet/) -- formerly the first mobile engineer at Uber and current founder of Flutter user onboarding startup [fluo.dev](https://fluo.dev/) -- explained this difference to me:

[![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd66124d8-105c-48f6-a5f7-816f861ae7e8_1600x804.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd66124d8-105c-48f6-a5f7-816f861ae7e8_1600x804.png)

*Summarizing the differences between the three platforms. The mental model shared by [Jordan Bonnet](https://www.linkedin.com/in/jordanbonnet/), cofounder of [fluo.dev](https://fluo.dev/)*

#### Performance: where Flutter flies