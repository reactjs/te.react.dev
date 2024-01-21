---
title: React ను ఇప్పటికే ఉన్న ప్రాజెక్ట్‌కు జోడించండి
---

<Intro>

మీరు ఇప్పటికే ఉన్న మీ ప్రాజెక్ట్‌కి కొంత ఇంటరాక్టివిటీని జోడించాలనుకుంటే, దాన్ని React లో మళ్ళీ రాసే అవసరం లేడు. మీ ఉన్న స్టాక్‌లో React ను జోడించి, ఇంటరాక్టివ్ React కాంపోనెంట్లను మీరు ఎక్కడైనా రెండర్ చేయవచ్చు.

</Intro>

<Note>

**మీరు React ను లోకల్ గా వాడాలి అనుకొంటే [Node.js](https://nodejs.org/en/) ను ఇన్స్టాల్ చేసుకోవలసి ఉంటుంది.** మీరు [React ను ఆన్‌లైన్‌లో ప్రయత్నించండి](/learn/installation#try-react) లేదా సాధారణ HTML పేజీతో ప్రయత్నించవచ్చు, కానీ వాస్తవానికి మీరు ప్రాజెక్ట్ డెవలప్మెంట్కు వాడాలనుకునే JavaScript టూలింగ్ కు Node.js అవసరం.

</Note>

## మీ ప్రస్తుత వెబ్‌సైట్ యొక్క మొత్తం సబ్‌రూట్ కోసం React ని ఉపయోగించడం {/*using-react-for-an-entire-subroute-of-your-existing-website*/}

అనుకొందాం మీకు ఇప్పటికే `example.com` లో ఒక వెబ్ యాప్‌ ఉంది, కానీ అది మరొక సర్వర్ టెక్నాలజీతో నిర్మించబడింది (ఉదాహరణకు Rails), మరియు మీరు `example.com/some-app/` లాంటి అన్ని మార్గాలను పూర్తిగా React తో అమలు చేయాలనుకుంటున్నారు.

దీన్ని సెటప్ చేయడానికి మీరు దిగువ స్టెప్స్ ను  అనుసరించాలని మేము సిఫార్సు చేస్తున్నాము:

1. [React ఆధారిత ఫ్రేమ్‌వర్క్‌లలో](/learn/start-a-new-react-project) ఒకదాన్ని ఉపయోగించి **మీ యాప్‌లోని React భాగాన్ని రూపొందించండి**.
2. మీ ఫ్రేమ్‌వర్క్ యొక్క కాన్ఫిగరేషన్‌లో **`/some-app` ని *base path* గా స్పెసిఫ్య్ చేయండి** (ఉదాహరణకు: [Next.js](https://nextjs.org/docs/api-reference/next.config.js/basepath), [Gatsby](https://www.gatsbyjs.com/docs/how-to/previews-deploys-hosting/path-prefix/)).
3. మీ React యాప్లోని `/some-app/` కింద ఉన్న అన్ని రిక్వెస్టులను స్వీకరించడానికి **మీ సర్వర్ లేదా ప్రాక్సీని కాన్ఫిగర్ చేయండి**.

మీ యాప్‌లోని React భాగం ఆ ఫ్రేమ్‌వర్క్‌లలో రూపొందించబడిన [ఉత్తమ అభ్యాసాల నుండి ప్రయోజనం పొందగలదని](/learn/start-a-new-react-project#can-i-use-react-without-a-framework) ఇది నిర్ధారిస్తుంది.

చాలా వరకు React-ఆధారిత ఫ్రేమ్‌వర్క్‌లు ఫుల్-స్టాక్‌గా ఉంటాయి మరియు మీ React యాప్ ను సర్వర్ యొక్క ప్రయోజనాన్ని పొందేలా చేస్తుంది. అయినప్పటికీ, మీరు సర్వర్‌లో JavaScript ని అమలు చేయలేకపోయినా లేదా చేయకూడదనుకున్నా మీరు అదే విధానాన్ని ఉపయోగించవచ్చు. ఆ సందర్భంలో, `/some-app/` వద్ద HTML/CSS/JS ఎక్సపోర్ట్ (Next.js కోసం [`next export` అవుట్‌పుట్](https://nextjs.org/docs/advanced-features/static-html-export), Gatsby కోసం డిఫాల్ట్) ని బదులుగా వాడండి.

## మీ ప్రస్తుత పేజీలో కొంత భాగం కోసం React ని ఉపయోగించడం {/*using-react-for-a-part-of-your-existing-page*/}

మీరు ఇప్పటికే మరొక సాంకేతికతతో రూపొందించిన పేజీని కలిగి ఉన్నారని అనుకుందాం (Rails వంటి సర్వర్ లేదా Backbone వంటి క్లయింట్), మరియు మీరు ఆ పేజీలో ఎక్కడైనా ఇంటరాక్టివ్ React భాగాలను రెండర్ చేయాలనుకుంటున్నారు. React ని ఇంటిగ్రేట్ చేయడానికి ఇది ఒక సాధారణ మార్గం--వాస్తవానికి, చాలా సంవత్సరాలుగా Meta లో చాలా వరకు React వినియోగం ఇలాగే జరుగుతోంది!

మీరు దీన్ని రెండు స్టెప్స్ లో చేయవచ్చు:

1. [JSX సింటాక్స్‌](/learn/writing-markup-with-jsx) ని ఉపయోగించడానికి మిమ్మల్ని అనుమతించే **JavaScript ఎన్విరాన్‌మెంట్‌ను సెటప్ చేయండి**, మీ కోడ్‌ను [`import`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) / [`export`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) సింటాక్స్‌తో మాడ్యూల్స్‌గా విభజించండి మరియు [npm](https://www.npmjs.com/) ప్యాకేజీ రిజిస్ట్రీ నుండి ప్యాకేజీలను ఉపయోగించండి (ఉదాహరణకు, React).
2. మీ React కాంపోనెంట్‌లను మీరు మీ పేజీలో ఎక్కడ చూడాలనుకుంటున్నారో **అక్కడ రెండర్ చేయండి**.

ఖచ్చితమైన విధానం మాత్రం ఇప్పటికే ఉన్న మీ పేజీ సెటప్‌పై ఆధారపడి ఉంటుంది, కాబట్టి కొన్ని వివరాలను చూద్దాం.

### స్టెప్ 1: మాడ్యులర్ JavaScript ఎన్విరాన్మెంట్ను సెటప్ చేయండి {/*step-1-set-up-a-modular-javascript-environment*/}

మాడ్యులర్ JavaScript ఎన్విరాన్మెంట్ మీ React కాంపోనెంట్‌లను ఇండివిడ్యుఅల్ ఫైల్‌లలో వ్రాయడానికి మిమ్మల్ని అనుమతిస్తుంది, ఇది మీ కోడ్ మొత్తాన్ని ఒకే ఫైల్‌లో రాయడానికి భిన్నంగా ఉంటుంది. [npm](https://www.npmjs.com/) రిజిస్ట్రీలో ఇతర డెవలపర్‌లు పబ్లిష్ చేసిన అన్ని అద్భుతమైన ప్యాకేజీలను ఉపయోగించడానికి కూడా ఇది మిమ్మల్ని అనుమతిస్తుంది—React‌ తో సహా! మీరు దీన్ని ఎలా చేస్తారు అనేది మీ ప్రస్తుత సెటప్‌పై ఆధారపడి ఉంటుంది:

* **మీ యాప్ ఇప్పటికే `import` స్టేట్‌మెంట్‌లను ఉపయోగించే ఫైల్‌లుగా విభజించబడి ఉంటే**, మీరు ఇప్పటికే ఉన్న సెటప్‌ను ఉపయోగించడానికి ప్రయత్నించండి. మీ JS కోడ్‌లో `<div />` వ్రాయడం వలన సింటాక్స్ ఎర్రర్ ఏర్పడిందో లేదో తనిఖీ చేయండి. ఒకవేళ సింటాక్స్ ఎర్రర్ వచ్చిందంటే, మీరు [మీ JavaScript కోడ్‌ని Babel తో మార్చవలసి ఉంటుంది](https://babeljs.io/setup) మరియు JSX ని ఉపయోగించడానికి [Babel React ప్రీసెట్‌](https://babeljs.io/docs/babel-preset-react) ను వాడాలి.

* **మీ యాప్‌లో JavaScript మాడ్యూల్‌లను కంపైల్ చేయడానికి ఇప్పటికే సెటప్ చేయకపోతే**, దానిని [Vite](https://vitejs.dev/) తో సెటప్ చేయండి. Vite కమ్యూనిటీలో Rails, Django మరియు Laravel తో సహా [అనేక బ్యాకెండ్ ఫ్రేమ్‌వర్క్‌లతో ఇంటెగ్రేషన్లను కలిగి ఉంది](https://github.com/vitejs/awesome-vite#integrations-with-backends). మీ బ్యాకెండ్ ఫ్రేమ్‌వర్క్ ఈ జాబితాలో లేకపోతే, మీ బ్యాకెండ్‌తో Vite బిల్డ్‌లను మాన్యువల్‌గా ఇంటిగ్రేట్ చేయడానికి [ఈ గైడ్‌ని అనుసరించండి](https://vitejs.dev/guide/backend-integration.html).

మీ సెటప్ పని చేస్తుందో లేదో తెలుసుకోడానికి, ఈ కమాండ్ని మీ ప్రాజెక్ట్ ఫోల్డర్‌లో రన్ చేయండి:

<TerminalBlock>
npm install react react-dom
</TerminalBlock>

ఆపై మీ ప్రధాన JavaScript ఫైల్ టాప్లో ఈ కోడ్ లైన్‌లను జోడించండి (దీనిని `index.js` లేదా `main.js` అని పిలవవచ్చు):

<Sandpack>

```html index.html hidden
<!DOCTYPE html>
<html>
  <head><title>My app</title></head>
  <body>
    <!-- మీ ప్రస్తుత పేజీ కంటెంట్ (ఈ ఉదాహరణలో, ఇది రీప్లేస్ చేయబడుతుంది) -->
  </body>
</html>
```

```js src/index.js active
import { createRoot } from 'react-dom/client';

// ఇప్పటికే ఉన్న HTML కంటెంట్‌ను క్లియర్ చేయండి
document.body.innerHTML = '<div id="app"></div>';

// బదులుగా మీ React కాంపోనెంట్‌ను రెండర్ చేయండి
const root = createRoot(document.getElementById('app'));
root.render(<h1>Hello, world</h1>);
```

</Sandpack>

మీ పేజీలోని మొత్తం కంటెంట్‌ను "Hello, World!" తో రిప్లేస్ చేయబడినట్లయితే, ప్రతిదీ అనుకొన్నట్లే పని చేస్తుంది! దయచేసి చదువుతూ ఉండండి.

<Note>

మాడ్యులర్ JavaScript ఎన్విరాన్మెంట్‌ని ఇప్పటికే ఉన్న ప్రాజెక్ట్‌లో మొదటిసారిగా ఇంటిగ్రేట్ చేయడం కొంచెం భయంగా అనిపించవచ్చు, కానీ అది విలువైనదే! మీరు ఏకదైనా చిక్కుకుపోయినట్లయితే, మా [కమ్యూనిటీ రిసోర్సెస్](/community) లేదా [Vite Chat](https://chat.vitejs.dev/) ని ఉపయోగించండి.

</Note>

### స్టెప్ 2: పేజీలో ఎక్కడైనా React భాగాలను రెండర్ చేయండి {/*step-2-render-react-components-anywhere-on-the-page*/}

మునుపటి స్టెప్లో, మీరు ఈ కోడ్‌ని మీ ప్రధాన ఫైల్లో టాప్లో ఉంచారు:

```js
import { createRoot } from 'react-dom/client';

// ఇప్పటికే ఉన్న HTML కంటెంట్‌ను క్లియర్ చేయండి
document.body.innerHTML = '<div id="app"></div>';

// బదులుగా మీ React కాంపోనెంట్‌ను రెండర్ చేయండి
const root = createRoot(document.getElementById('app'));
root.render(<h1>Hello, world</h1>);
```

వాస్తవానికి, మీరు ఇప్పటికే ఉన్న HTML కంటెంట్‌ను క్లియర్ చేయకూడదనుకుంటున్నారు!

ఈ కోడ్‌ని తొలగించండి.

బదులుగా, మీరు బహుశా మీ HTML లోని నిర్దిష్ట ప్రదేశాలలో మీ React భాగాలను రెండర్ చేయాలనుకుంటున్నారు. మీ HTML పేజీని ఓపెన్ చేసి (లేదా దానిని రూపొందించే సర్వర్ టెంప్లేట్లను ఓపెన్ చేసి) మరియు ఏదైనా ట్యాగ్‌కి యూనిక్ [`id`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/id) అట్రిబ్యూట్‌ని జోడించండి, ఉదాహరణకు:

```html
<!-- ... మీ HTML లో ఎక్కడో ఉంది ... -->
<nav id="navigation"></nav>
<!-- ... మరింత HTML ... -->
```

ఇది [`document.getElementById`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById) తో ఆ HTML ఎలిమెంట్‌ను కనుగొని, దాన్ని [`createRoot`](/reference/react-dom/client/createRoot) కి పంపుతుంది, తద్వారా మీరు లోపల మీ స్వంత React కాంపోనెంట్‌ను రెండర్ చేయవచ్చు:

<Sandpack>

```html index.html
<!DOCTYPE html>
<html>
  <head><title>My app</title></head>
  <body>
    <p>This paragraph is a part of HTML.</p>
    <nav id="navigation"></nav>
    <p>This paragraph is also a part of HTML.</p>
  </body>
</html>
```

```js src/index.js active
import { createRoot } from 'react-dom/client';

function NavigationBar() {
  // TODO: వాస్తవానికి నావిగేషన్ బార్‌ ని ఇంప్లీమెంట్ చేయండి
  return <h1>Hello from React!</h1>;
}

const domNode = document.getElementById('navigation');
const root = createRoot(domNode);
root.render(<NavigationBar />);
```

</Sandpack>

`index.html` నుండి అసలు HTML కంటెంట్ ఎలా భద్రపరచబడిందో గమనించండి, కానీ మీ స్వంత `NavigationBar` React కంపోనెంట్ ఇప్పుడు మీ HTML నుండి `<nav id="navigation">` లో కనిపిస్తుంది. ఇప్పటికే ఉన్న HTML పేజీలో React కంపోనెంట్లను రెండరింగ్ చేయడం గురించి మరింత తెలుసుకోవడానికి [`createRoot` వినియోగ డాక్యుమెంటేషన్‌ను](/reference/react-dom/client/createRoot#rendering-a-page-partially-built-with-react) చదవండి.

మీరు ఇప్పటికే ఉన్న ప్రాజెక్ట్‌లో React ని స్వీకరించినప్పుడు, చిన్న ఇంటరాక్టివ్ కాంపోనెంట్‌లతో (ఉదాహరణకు బటన్లు) ప్రారంభించడం సాధారణం, ఆపై మీ పేజీ మొత్తం React తో నిర్మించబడే వరకు క్రమంగా “పైకి కదులుతూ” ఉంటుంది. మీరు ఎప్పుడైనా ఆ పాయింట్కి చేరుకున్నట్లయితే, React నుండి ఎక్కువ ప్రయోజనం పొందడానికి వెంటనే [React ఫ్రేమ్‌వర్క్‌కి](/learn/start-a-new-react-project) మైగ్రేట్ అవ్వమని మేము సిఫార్సు చేస్తున్నాము.

## ఇప్పటికే ఉన్న నేటివ్ మొబైల్ యాప్‌లో React Native‌ ని ఉపయోగించడం {/*using-react-native-in-an-existing-native-mobile-app*/}

[React Native](https://reactnative.dev/) ను ఇప్పటికే ఉన్న నేటివ్ యాప్‌లలో కూడా క్రమంగా ఇంటిగ్రేట్ చేయవచ్చు. మీరు Android (Java లేదా Kotlin) లేదా iOS (Objective-C లేదా Swift) లో ఇప్పటికే నేటివ్ యాప్‌ని కలిగి ఉంటే, దానికి React Native స్క్రీన్‌ని జోడించడానికి [ఈ గైడ్‌ని అనుసరించండి](https://reactnative.dev/docs/integration-with-existing-apps).
