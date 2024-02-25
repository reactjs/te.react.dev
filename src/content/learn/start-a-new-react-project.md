---
title: కొత్త React ప్రాజెక్ట్‌ను ప్రారంభించండి
---

<Intro>

If you want to build a new app or a new website fully with React, we recommend picking one of the React-powered frameworks popular in the community.

</Intro>


You can use React without a framework, however we’ve found that most apps and sites eventually build solutions to common problems such as code-splitting, routing, data fetching, and generating HTML. These problems are common to all UI libraries, not just React.

By starting with a framework, you can get started with React quickly, and avoid essentially building your own framework later.

<DeepDive>

#### Can I use React without a framework? {/*can-i-use-react-without-a-framework*/}

You can definitely use React without a framework--that's how you'd [use React for a part of your page.](/learn/add-react-to-an-existing-project#using-react-for-a-part-of-your-existing-page) **However, if you're building a new app or a site fully with React, we recommend using a framework.**

Here's why.

Even if you don't need routing or data fetching at first, you'll likely want to add some libraries for them. As your JavaScript bundle grows with every new feature, you might have to figure out how to split code for every route individually. As your data fetching needs get more complex, you are likely to encounter server-client network waterfalls that make your app feel very slow. As your audience includes more users with poor network conditions and low-end devices, you might need to generate HTML from your components to display content early--either on the server, or during the build time. Changing your setup to run some of your code on the server or during the build can be very tricky.

**These problems are not React-specific. This is why Svelte has SvelteKit, Vue has Nuxt, and so on.** To solve these problems on your own, you'll need to integrate your bundler with your router and with your data fetching library. It's not hard to get an initial setup working, but there are a lot of subtleties involved in making an app that loads quickly even as it grows over time. You'll want to send down the minimal amount of app code but do so in a single client–server roundtrip, in parallel with any data required for the page. You'll likely want the page to be interactive before your JavaScript code even runs, to support progressive enhancement. You may want to generate a folder of fully static HTML files for your marketing pages that can be hosted anywhere and still work with JavaScript disabled. Building these capabilities yourself takes real work.

**React frameworks on this page solve problems like these by default, with no extra work from your side.** They let you start very lean and then scale your app with your needs. Each React framework has a community, so finding answers to questions and upgrading tooling is easier. Frameworks also give structure to your code, helping you and others retain context and skills between different projects. Conversely, with a custom setup it's easier to get stuck on unsupported dependency versions, and you'll essentially end up creating your own framework—albeit one with no community or upgrade path (and if it's anything like the ones we've made in the past, more haphazardly designed).

If your app has unusual constraints not served well by these frameworks, or you prefer to solve these problems yourself, you can roll your own custom setup with React. Grab `react` and `react-dom` from npm, set up your custom build process with a bundler like [Vite](https://vitejs.dev/) or [Parcel](https://parceljs.org/), and add other tools as you need them for routing, static generation or server-side rendering, and more.

</DeepDive>

## Production-grade React frameworks {/*production-grade-react-frameworks*/}

These frameworks support all the features you need to deploy and scale your app in production and are working towards supporting our [full-stack architecture vision](#which-features-make-up-the-react-teams-full-stack-architecture-vision). All of the frameworks we recommend are open source with active communities for support, and can be deployed to your own server or a hosting provider. If you’re a framework author interested in being included on this list, [please let us know](https://github.com/reactjs/react.dev/issues/new?assignees=&labels=type%3A+framework&projects=&template=3-framework.yml&title=%5BFramework%5D%3A+).

### Next.js {/*nextjs-pages-router*/}

**[Next.js' Pages Router](https://nextjs.org/) is a full-stack React framework.** It's versatile and lets you create React apps of any size--from a mostly static blog to a complex dynamic application. To create a new Next.js project, run in your terminal:

<TerminalBlock>
npx create-next-app@latest
</TerminalBlock>

If you're new to Next.js, check out the [learn Next.js course.](https://nextjs.org/learn)

Next.js is maintained by [Vercel](https://vercel.com/). You can [deploy a Next.js app](https://nextjs.org/docs/app/building-your-application/deploying) to any Node.js or serverless hosting, or to your own server. Next.js also supports a [static export](https://nextjs.org/docs/pages/building-your-application/deploying/static-exports) which doesn't require a server.

### Remix {/*remix*/}

**[Remix](https://remix.run/) is a full-stack React framework with nested routing.** It lets you break your app into nested parts that can load data in parallel and refresh in response to the user actions. To create a new Remix project, run:

<TerminalBlock>
npx create-remix
</TerminalBlock>

If you're new to Remix, check out the Remix [blog tutorial](https://remix.run/docs/en/main/tutorials/blog) (short) and [app tutorial](https://remix.run/docs/en/main/tutorials/jokes) (long).

Remix is maintained by [Shopify](https://www.shopify.com/). When you create a Remix project, you need to [pick your deployment target](https://remix.run/docs/en/main/guides/deployment). You can deploy a Remix app to any Node.js or serverless hosting by using or writing an [adapter](https://remix.run/docs/en/main/other-api/adapter).

### Gatsby {/*gatsby*/}

**[Gatsby](https://www.gatsbyjs.com/) is a React framework for fast CMS-backed websites.** Its rich plugin ecosystem and its GraphQL data layer simplify integrating content, APIs, and services into one website. To create a new Gatsby project, run:

<TerminalBlock>
npx create-gatsby
</TerminalBlock>

If you're new to Gatsby, check out the [Gatsby tutorial.](https://www.gatsbyjs.com/docs/tutorial/)

Gatsby is maintained by [Netlify](https://www.netlify.com/). You can [deploy a fully static Gatsby site](https://www.gatsbyjs.com/docs/how-to/previews-deploys-hosting) to any static hosting. If you opt into using server-only features, make sure your hosting provider supports them for Gatsby.

### Expo (for native apps) {/*expo*/}

**[Expo](https://expo.dev/) is a React framework that lets you create universal Android, iOS, and web apps with truly native UIs.** It provides an SDK for [React Native](https://reactnative.dev/) that makes the native parts easier to use. To create a new Expo project, run:

<TerminalBlock>
npx create-expo-app
</TerminalBlock>

If you're new to Expo, check out the [Expo tutorial](https://docs.expo.dev/tutorial/introduction/).

Expo is maintained by [Expo (the company)](https://expo.dev/about). Building apps with Expo is free, and you can submit them to the Google and Apple app stores without restrictions. Expo additionally provides opt-in paid cloud services.

## Bleeding-edge React frameworks {/*bleeding-edge-react-frameworks*/}

React ని ఇంప్రూవ్ చేయడం ఎలా కొనసాగించాలో మేము అన్వేషిస్తున్నప్పుడు, React ని ఫ్రేమ్‌వర్క్‌లతో (ప్రత్యేకంగా, రూటింగ్, బండ్లింగ్ మరియు సర్వర్ సాంకేతికతలతో) మరింత క్లోజ్గా ఇంటిగ్రేట్ చేయడం అనేది React యూజర్‌లకు మెరుగైన యాప్‌లను రూపొందించడంలో సహాయపడుతుంది కాబట్టి ఇది మా అతిపెద్ద అవకాశం అని మేము గ్రహించాము. Next.js బృందం ఫ్రేమ్‌వర్క్‌ను రీసెర్చ్ చేయడం, డెవలప్ చేయడం, ఇంటిగ్రేట్ చేయడం మరియు టెస్టింగ్లో మాతో సహకరించడానికి అంగీకరించింది తద్వారా బ్లీడింగ్-ఎడ్జ్ React ఫీచర్లను అందిస్తుంది ఉదాహరణకు [React Server Components.](/blog/2023/03/22/react-labs-what-we-have-been-working-on-march-2023#react-server-components)

ఈ ఫీచర్‌లు ప్రతిరోజూ ప్రొడక్షన్-రెడీగా ఉండటానికి దగ్గరవుతున్నాయి మరియు మేము వాటిని ఇంటిగ్రేట్ చేయడం గురించి ఇతర బండ్లర్ మరియు ఫ్రేమ్‌వర్క్ డెవలపర్‌లతో చర్చలు జరుపుతున్నాము. ఒకటి లేదా రెండు సంవత్సరాలలో, ఈ పేజీలో జాబితా చేయబడిన అన్ని ఫ్రేమ్‌వర్క్‌లు ఈ ఫీచర్లకు పూర్తి సపోర్ట్ ఇస్తాయి అని మా ఆశ. (మీరు ఫ్రేమ్‌వర్క్ రచయిత అయితే మరియు ఈ ఫీచర్లను ఎక్స్పరిమెంట్ చేయడానికి మరియు మాతో సహకరించడానికి ఆసక్తి కలిగి ఉంటే, దయచేసి మమ్మల్ని సంప్రదించండి!)

### Next.js (App Router) {/*nextjs-app-router*/}

**[Next.js యొక్క App Router](https://nextjs.org/docs) అనేది React టీమ్ యొక్క ఫుల్-స్టాక్ ఆర్కిటెక్చర్ విజన్‌ని నెరవేర్చడానికి ఉద్దేశించిన Next.js APIల రీడిజైన్.** ఇది సర్వర్‌లో లేదా బిల్డ్ సమయంలో కూడా రన్ చేసే అసిన్క్రోనస్ కంపోనెంట్లలో డేటాను ఫెట్చ్ చేయడానికి మిమ్మల్ని అనుమతిస్తుంది.

Next.js ను [Vercel](https://vercel.com/) మైంటైన్ చేస్తుంది. మీరు ఏదైనా Node.js లేదా సర్వర్‌లెస్ హోస్టింగ్‌కి లేదా మీ స్వంత సర్వర్‌లో [Next.js యాప్‌ని డిప్లాయ్ చేయవచ్చు.](https://nextjs.org/docs/app/building-your-application/deploying) Next.js సర్వర్ అవసరం లేని [స్టాటిక్ ఎక్స్పోర్ట్](https://nextjs.org/docs/app/building-your-application/deploying/static-exports) కి కూడా సపోర్ట్ ఇస్తుంది.

<DeepDive>

#### React టీమ్ ఫుల్-స్టాక్ ఆర్కిటెక్చర్ విజన్‌ను ఏ ఫీచర్లు రూపొందించాయి? {/*which-features-make-up-the-react-teams-full-stack-architecture-vision*/}

Next.js యొక్క App Router బండ్లర్ అఫీషియల్ [React Server Components స్పెసిఫికేషన్‌](https://github.com/reactjs/rfcs/blob/main/text/0188-server-components.md) ను పూర్తిగా ఇంప్లీమెంట్ చేస్తుంది. ఇది బిల్డ్-టైమ్, సర్వర్-ఓన్లీ మరియు ఇంటరాక్టివ్ కాంపోనెంట్‌లను ఒకే React ట్రీలో కలిపి వాడడానికి మిమ్మల్ని అనుమతిస్తుంది.

ఉదాహరణకు, మీరు ఒక సర్వర్-ఓన్లీ React కాంపోనెంట్‌ను డేటాబేస్ నుండి లేదా ఫైల్ నుండి రీడ్ చేసే `async` ఫంక్షన్‌గా వ్రాయవచ్చు. అప్పుడు మీరు దాని నుండి మీ ఇంటరాక్టివ్ కంపోనెంట్లకు డేటాను పంపవచ్చు:

```js
// ఈ కంపోనెంట్ సర్వర్‌లో (లేదా బిల్డ్ సమయంలో) *మాత్రమే* రన్ అవుతుంది.
async function Talks({ confId }) {
  // 1. మీరు సర్వర్‌లో ఉన్నారు, కాబట్టి మీరు మీ డేటా లేయర్‌తో కమ్యూనికేట్ అవ్వచ్చు. API ఎండ్ పాయింట్ అవసరం లేదు.
  const talks = await db.Talks.findAll({ confId });

  // 2. ఎంత రెండరింగ్ లాజిక్ ని ఐనా యాడ్ చేయండి. ఇది మీ JavaScript బండిల్‌ను పెద్దదిగా చేయదు.
  const videos = talks.map(talk => talk.video);

  // 3. బ్రౌజర్‌లో రన్ అయ్యే కంపోనెంట్లకు డేటాను పంపండి.
  return <SearchableVideoList videos={videos} />;
}
```

Next.js యొక్క App Router [సస్పెన్స్ (Suspense) తో డేటా ఫెట్చింగ్ చేయడానికి](/blog/2022/03/29/react-v18#suspense-in-data-frameworks) సపోర్ట్ ఇస్తుంది. ఇది మీ React ట్రీలో డైరెక్టుగా UI లోని వివిధ భాగాల కోసం లోడింగ్ స్టేట్ని (ఉదాహరణకు స్కెలిటన్ ప్లేస్‌హోల్డర్) స్పెసిఫ్య్ చేయడానికి మిమ్మల్ని అనుమతిస్తుంది:

```js
<Suspense fallback={<TalksLoading />}>
  <Talks confId={conf.id} />
</Suspense>
```

సర్వర్ కంపోనెంట్స్ మరియు సస్పెన్స్ React యొక్క ఫీచర్లు, Next.js వి కావు. అయినప్పటికీ, వాటిని ఫ్రేమ్‌వర్క్ లెవెల్ లో అడాప్ట్ చేసుకోవడానికి కొనుగోలు మరియు నాన్-ట్రివియల్ ఇంప్లిమెంటేషన్ వర్క్ అవసరం. ప్రస్తుతానికి, Next.js యొక్క App Router అత్యంత పూర్తి ఇంప్లిమెంటేషన్. తదుపరి జనరేషన్ ఫ్రేమ్‌వర్క్‌లలో ఈ ఫీచర్‌లను సులభంగా అమలు చేయడానికి React బృందం బండ్లర్ డెవలపర్‌లతో కలిసి పని చేస్తోంది.

</DeepDive>
