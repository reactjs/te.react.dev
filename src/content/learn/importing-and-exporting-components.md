---
title: కంపోనెంట్లను ఇంపోర్ట్ మరియు ఎక్స్‌పోర్ట్ చేయడం
---

<Intro>

కంపోనెంట్ల మ్యాజిక్ వాటి రీయూజబులిటీలో ఉంది: మీరు ఇతర కంపోనెంట్లతో కలిపిన కంపోనెంట్లను సృష్టించవచ్చు. కానీ మీరు ఎక్కువ కంపోనెంట్లను నెస్ట్ చేసినప్పుడు, వాటిని వేరువేరు ఫైళ్లలో విభజించడం ప్రారంభించటం ఆలోచనీయంగా ఉంటుంది. ఇది మీ ఫైళ్లను సులభంగా స్కాన్ చేయగలిగేలా చేస్తుంది మరియు కంపోనెంట్లను మరిన్ని ప్రదేశాలలో రీయూజబుల్ చేసుకునేందుకు అనుకూలంగా ఉంటుంది.

</Intro>

<YouWillLearn>

* రూట్ కంపోనెంట్ ఫైల్ అంటే ఏమిటో
* కంపోనెంట్లను ఇంపోర్ట్ చేసుకోవడం మరియు ఎక్స్‌పోర్ట్ చేయడం ఎలా
* డిఫాల్ట్ మరియు నేమ్డ్ ఇంపోర్ట్ మరియు ఎక్స్‌పోర్ట్ ఎప్పుడు మరియు ఎలా ఉపయోగించాలో
* ఒక ఫైల్ నుండి అనేక కంపోనెంట్లను ఇంపోర్ట్ చేయడం మరియు ఎక్స్‌పోర్ట్ చేయడం ఎలా
* కంపోనెంట్లను అనేక ఫైళ్లలో విభజించడం ఎలా చేయాలో

</YouWillLearn>

## రూట్ కంపోనెంట్ ఫైల్ {/*the-root-component-file*/}

[మీ మొదటి కంపోనెంట్](/learn/your-first-component) లో, మీరు `Profile` అనే కంపోనెంట్ మరియు దానిని రెండర్ చేసే `Gallery` అనే కంపోనెంట్ సృష్టించారు:

<Sandpack>

```js
function Profile() {
  return (
    <img
      src="https://i.imgur.com/MK3eW3As.jpg"
      alt="Katherine Johnson"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

ఇవి ప్రస్తుతం **రూట్ కంపోనెంట్ ఫైల్** లో ఉన్నాయి, ఈ ఉదాహరణలో `App.js`. మీ సెటప్‌పై ఆధారపడి, మీ రూట్ కంపోనెంట్ వేరే ఫైల్‌లో ఉండవచ్చు. మీరు Next.js లాంటి ఫైల్ ఆధారిత రూటింగ్ ఫ్రేమ్‌వర్క్ ఉపయోగిస్తే, ప్రతి పేజీకి మీ రూట్ కంపోనెంట్ వేరుగా ఉంటుంది.

## కంపోనెంట్లను ఎక్స్‌పోర్ట్ మరియు ఇంపోర్ట్ చేయడం {/*exporting-and-importing-a-component*/}

మీరు భవిష్యత్తులో ల్యాండింగ్ స్క్రీన్‌ను మార్చి అక్కడ ఒక సైన్స్ పుస్తకాల జాబితా ఉంచాలని అనుకుంటే? లేదా అన్ని ప్రొఫైల్స్‌ను మరొకచోట ఉంచాలనుకుంటే? `Gallery` మరియు `Profile` ను రూట్ కంపోనెంట్ ఫైల్ నుండి బయటకు తరలించడం అవసరం. ఇది వాటిని మరింత మాడ్యులర్‌గా, ఇతర ఫైళ్లలో రీయూజబుల్ చేయడానికి అనుకూలంగా చేస్తుంది. కంపోనెంట్‌ను తరలించడానికి మూడు దశలు ఉన్నాయి:

1. **కొత్త** JS ఫైల్ ను కంపోనెంట్లను ఉంచడానికి సృష్టించండి.
2. ఆ ఫైల్ నుండి మీ ఫంక్షన్ కంపోనెంట్‌ను **ఎక్స్‌పోర్ట్** చేయండి ([డిఫాల్ట్](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/export#using_the_default_export) లేదా [నేమ్డ్](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/export#using_named_exports) ఎక్స్‌పోర్ట్స్‌ను ఉపయోగించి).
3. మీరు కంపోనెంట్‌ను ఉపయోగించే ఫైల్‌లో **ఇంపోర్ట్** చేసుకోండి ((తదనుగుణంగా [డిఫాల్ట్](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/import#importing_defaults) లేదా [నేమ్డ్](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/import#import_a_single_export_from_a_module) ఇంపోర్ట్‌ల పద్ధతిని ఉపయోగించండి).

ఇక్కడ `Profile` మరియు `Gallery` రెండూ `App.js` నుండి బయటకు తీసి కొత్త ఫైల్ `Gallery.js` లో ఉంచబడ్డాయి. ఇప్పుడు మీరు `App.js` లో `Gallery.js` నుండి `Gallery` ని ఇంపోర్ట్ చేసుకోవచ్చు:

<Sandpack>

```js src/App.js
import Gallery from './Gallery.js';

export default function App() {
  return (
    <Gallery />
  );
}
```

```js src/Gallery.js
function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

ఈ ఉదాహరణ ఇప్పుడు రెండు కంపోనెంట్ ఫైళ్లలో విభజించబడింది:

1. `Gallery.js`:
     - `Profile` కంపోనెంట్‌ను డిఫైన్ చేస్తుంది, ఇది అదే ఫైల్‌లో మాత్రమే ఉపయోగించబడుతుంది మరియు ఎక్స్‌పోర్ట్ చేయబడదు.
     - `Gallery` కంపోనెంట్‌ను **డిఫాల్ట్ ఎక్స్‌పోర్ట్** గా ఎక్స్‌పోర్ట్‌ చేస్తుంది.
2. `App.js`:
     - `Gallery.js` నుండి `Gallery` ను **డిఫాల్ట్ ఇంపోర్ట్** గా ఇంపోర్ట్ చేసుకుంటుంది.
     - రూట్ App కంపోనెంట్‌ను **డిఫాల్ట్ ఎక్స్‌పోర్ట్** గా ఎక్స్‌పోర్ట్‌ చేస్తుంది.


<Note>

మీరు `.js` ఫైల్ ఎక్స్‌టెన్షన్ లేకుండా ఉండే ఫైళ్లను ఎదుర్కొన్నట్లయితే, అవి ఈ విధంగా ఉంటాయి:

```js 
import Gallery from './Gallery';
```

React తో, `'./Gallery.js'` లేదా `'./Gallery'` రెండూ పని చేస్తాయి, అయితే మొదటి పద్ధతి [నేటివ్ ES మాడ్యూల్స్](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Modules) ఎలా పని చేస్తాయో దానికి దగ్గరగా ఉంటుంది.

</Note>

<DeepDive>

#### డిఫాల్ట్ ఎక్స్‌పోర్ట్స్ వర్సెస్ నేమ్డ్ ఎక్స్‌పోర్ట్స్ {/*default-vs-named-exports*/}

JavaScript లో వాల్యూస్‌ను ఎక్స్‌పోర్ట్ చేయడానికి రెండు ప్రధాన మార్గాలు ఉన్నాయి: డిఫాల్ట్ ఎక్స్‌పోర్ట్స్ మరియు నేమ్డ్ ఎక్స్‌పోర్ట్స్. ఇంతవరకు, మా ఉదాహరణలు కేవలం డిఫాల్ట్ ఎక్స్‌పోర్ట్స్ మాత్రమే ఉపయోగించాయి. కానీ మీరు వాటిలో ఒకటి లేదా రెండూ ఉపయోగించవచ్చు. **ఒక ఫైల్‌లో కేవలం ఒకే ఒక డిఫాల్ట్ ఎక్స్‌పోర్ట్ ఉండవచ్చు, కానీ మీరు అనుకున్నంత నేమ్డ్ ఎక్స్‌పోర్ట్స్ ఉంచవచ్చు.**

![డిఫాల్ట్ మరియు నేమ్డ్ ఎక్స్‌పోర్ట్స్](/images/docs/illustrations/i_import-export.svg)

మీరు మీ కంపోనెంట్‌ను ఎక్స్‌పోర్ట్ చేసే విధానం మీరు దాన్ని ఎలా ఇంపోర్ట్ చేయాలో నిర్ణయిస్తుంది. మీరు డిఫాల్ట్ ఎక్స్‌పోర్ట్‌ను నేమ్డ్ ఎక్స్‌పోర్ట్‌కి సరిపోలిన విధంగా ఇంపోర్ట్ చేయాలని ప్రయత్నిస్తే, ఎర్రర్ వస్తుంది! ఈ చార్ట్ మీకు సహాయం చేస్తుంది:

| సింటాక్స్           | ఎక్స్‌పోర్ట్ స్టేట్మెంట్                           | ఇంపోర్ట్ స్టేట్మెంట్                          |
| -----------      | -----------                                | -----------                               |
| డిఫాల్ట్  | `export default function Button() {}` | `import Button from './Button.js';`     |
| నేమ్డ్    | `export function Button() {}`         | `import { Button } from './Button.js';` |

మీరు ఒక _డిఫాల్ట్_ ఇంపోర్ట్ రాస్తే, మీరు import తర్వాత ఏ పేరైనా ఉంచవచ్చు. ఉదాహరణకు, మీరు `import Banana from './Button.js'` అని రాయవచ్చు మరియు అది మీకు అదే డిఫాల్ట్ ఎగుమతిని అందిస్తుంది. ప్రతికూలంగా, నేమ్డ్ ఇంపోర్ట్ లో, పేరు రెండు వైపులా సరిపోయేది కావాలి. అందుకే వాటిని _నేమ్డ్_ ఇంపోర్ట్ లు అని పిలుస్తారు!

**మొత్తం ఫైల్ ఒకే ఒక కంపోనెంట్‌ను ఎక్స్‌పోర్ట్ చేస్తే, డిఫాల్ట్ ఎక్స్‌పోర్ట్స్ సాధారణంగా ఉపయోగిస్తారు, మరియు అది అనేక కంపోనెంట్లు మరియు విలువలను ఎక్స్‌పోర్ట్ చేస్తే, నేమ్డ్ ఎక్స్‌పోర్ట్స్ ఉపయోగిస్తారు.** మీరు ఎంచుకున్న కోడింగ్ శైలి ఏదైనా అయినా, ఎల్లప్పుడూ మీ కంపోనెంట్ ఫంక్షన్స్ మరియు వాటిని కలిగి ఉన్న ఫైళ్ళకు అర్థవంతమైన పేర్లను ఇవ్వండి. పేరులు లేని కంపోనెంట్లు, ఉదాహరణకి `export default () => {}`, డీబగ్గింగ్‌ను కష్టతరంగా చేస్తాయి కనుక వాటిని ఉపయోగించడం ప్రోత్సహించదు.

</DeepDive>

## ఒకే ఫైల్ నుండి అనేక కంపోనెంట్లను ఎక్స్‌పోర్ట్ మరియు ఇంపోర్ట్ చేయడం {/*exporting-and-importing-multiple-components-from-the-same-file*/}

మీరు gallery బదులు ఒకే `Profile` చూపించాలని కోరుకుంటే ఏమిటి? మీరు `Profile` కంపోనెంట్‌ను కూడా ఎక్స్‌పోర్ట్ చేయవచ్చు. కానీ `Gallery.js` లో ఇప్పటికే డిఫాల్ట్ ఎక్స్‌పోర్ట్ ఉంది, మరియు మీరు _రెండు_ డిఫాల్ట్ ఎక్స్‌పోర్ట్స్ కలిగి ఉండలేరు. మీరు ఒక కొత్త ఫైల్‌ను డిఫాల్ట్ ఎక్స్‌పోర్ట్‌తో సృష్టించవచ్చు, లేదా `Profile` కోసం నేమ్డ్ ఎక్స్‌పోర్ట్‌ను జోడించవచ్చు. **ఒక ఫైల్‌లో కేవలం ఒక డిఫాల్ట్ ఎక్స్‌పోర్ట్ ఉండవచ్చు, కానీ అనేక నేమ్డ్ ఎక్స్‌పోర్ట్స్ ఉండవచ్చు!**

<Note>

డిఫాల్ట్ మరియు నేమ్డ్ ఎక్స్‌పోర్ట్స్ మధ్య గందరగోళాన్ని తగ్గించడానికి, కొంతమంది టీములు ఒకే శైలిని మాత్రమే (డిఫాల్ట్ లేదా నేమ్డ్) ఉపయోగించడం లేదా వాటిని ఒకే ఫైల్‌లో మిళితం చేయడం నుండి తప్పించుకుంటారు. మీకు ఏది సరైనదో అది చేయండి!

</Note>

మొదట, **ఎక్స్‌పోర్ట్** చేయండి `Profile` ని `Gallery.js` నుండి, నేమ్డ్ ఎక్స్‌పోర్ట్ ద్వారా (డిఫాల్ట్ కీవర్డ్‌ను ఉపయోగించకుండా):

```js
export function Profile() {
  // ...
}
```

తర్వాత, **ఇంపోర్ట్** చేయండి `Profile` ని `Gallery.js` నుండి `App.js` లో, నేమ్డ్ ఇంపోర్ట్ ద్వారా (కర్లీ బ్రేసెస్‌తో):

```js
import { Profile } from './Gallery.js';
```

చివరగా, **రెండర్** చేయండి `<Profile />` ని `App` కంపోనెంట్ నుండి:

```js
export default function App() {
  return <Profile />;
}
```

ఇప్పుడు `Gallery.js` లో రెండు ఎక్స్‌పోర్ట్ లు ఉన్నాయి: ఒక డిఫాల్ట్ Gallery ఎక్స్‌పోర్ట్, మరియు ఒక నేమ్డ్ `Profile` ఎక్స్‌పోర్ట్. `App.js` రెండింటినీ ఇంపోర్ట్ చేసుకుంటుంది. ఈ ఉదాహరణలో `<Profile />` ను `<Gallery />` గా ఎడిట్ చేసి, మళ్ళీ వెనక్కి మార్చడానికి ప్రయత్నించండి:

<Sandpack>

```js src/App.js
import Gallery from './Gallery.js';
import { Profile } from './Gallery.js';

export default function App() {
  return (
    <Profile />
  );
}
```

```js src/Gallery.js
export function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

ఇప్పుడు మీరు డిఫాల్ట్ మరియు నేమ్డ్ ఎక్స్‌పోర్ట్‌ల మిశ్రమాన్ని ఉపయోగిస్తున్నారు:

* `Gallery.js`:
  - `Profile` కంపోనెంట్‌ను **నేమ్డ్ ఎక్స్‌పోర్ట్ చేస్తుంది, దీనిని `Profile` అని పిలవబడుతుంది.**
  - `Gallery` కంపోనెంట్‌ను **డిఫాల్ట్ ఎక్స్‌పోర్ట్** గా ఎక్స్‌పోర్ట్ చేస్తుంది.
* `App.js`:
  - `Gallery.js` నుండి `Profile` ను **నేమ్డ్ ఇంపోర్ట్ చేసుకుంటుంది, దీనిని `Profile` అని పిలవబడుతుంది.**
  - `Gallery` ను `Gallery.js` నుండి **డిఫాల్ట్ ఇంపోర్ట్** గా ఇంపోర్ట్ చేసుకుంటుంది.
  - రూట్ `App` కంపోనెంట్‌ను **డిఫాల్ట్ ఎక్స్‌పోర్ట్** గా ఎక్స్‌పోర్ట్ చేస్తుంది.

<Recap>

ఈ పేజీలో మీరు నేర్చుకున్నవి::

* రూట్ కంపోనెంట్ ఫైల్ అంటే ఏమిటి
* ఒక కంపోనెంట్‌ను ఎలా ఇంపోర్ట్ మరియు ఎక్స్‌పోర్ట్ చేయాలి
* డిఫాల్ట్ మరియు నేమ్డ్ ఇంపోర్ట్స్ మరియు ఎక్స్‌పోర్ట్స్ ను ఎప్పుడు మరియు ఎలా ఉపయోగించాలి
* ఒకే ఫైల్ నుండి అనేక కంపోనెంట్లను ఎలా ఎక్స్‌పోర్ట్ చేయాలి

</Recap>



<Challenges>

#### కంపోనెంట్లను మరింత విభజించండి {/*split-the-components-further*/}

ప్రస్తుతం, `Gallery.js` రెండు `Profile` మరియు `Gallery` కంపోనెంట్లను ఎక్స్‌పోర్ట్ చేస్తుంది, ఇది కొంత గందరగోళంగా ఉంది.

`Profile` కంపోనెంట్‌ను దాని స్వంత `Profile.js` కు తరలించండి, మరియు తర్వాత `App` కంపోనెంట్‌ను మార్చి `<Profile />` మరియు `<Gallery />` ను వరుసగా రెండర్ చేయండి.

మీరు `Profile` కోసం డిఫాల్ట్ లేదా నేమ్డ్ ఎక్స్‌పోర్ట్‌ను ఉపయోగించవచ్చు, కానీ మీరు రెండు `App.js` మరియు `Gallery.js` లో సరైన ఇంపోర్ట్ సింట్యాక్స్‌ను ఉపయోగిస్తున్నారో చూడండి! మీరు పై డీప్ డైవ్ లోని చార్టును చూడవచ్చు:

| సింటాక్స్           | ఎక్స్‌పోర్ట్ స్టేట్‌మెంట్                           | ఇంపోర్ట్ స్టేట్‌మెంట్                          |
| -----------      | -----------                                | -----------                               |
| డిఫాల్ట్  | `export default function Button() {}` | `import Button from './Button.js';`     |
| నేమ్డ్    | `export function Button() {}`         | `import { Button } from './Button.js';` |

<Hint>

మీరు ఎక్కడ పిలవబడతాయో అక్కడ మీ కంపోనెంట్లను ఇంపోర్ట్ చేయడం మర్చిపోకండి. `Gallery` కూడా `Profile` ను ఉపయోగించదేమో?

</Hint>

<Sandpack>

```js src/App.js
import Gallery from './Gallery.js';
import { Profile } from './Gallery.js';

export default function App() {
  return (
    <div>
      <Profile />
    </div>
  );
}
```

```js src/Gallery.js active
// Move me to Profile.js!
export function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

```js src/Profile.js
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

మీరు ఒక రకమైన ఎక్స్‌పోర్ట్స్‌తో పని చేయగానే, ఇతర రకమైన ఎక్స్‌పోర్ట్స్‌తో కూడా పనిచేయాలని ప్రయత్నించండి.

<Solution>

ఇది నేమ్డ్ ఎక్స్‌పోర్ట్స్‌తో సమాధానం:

<Sandpack>

```js src/App.js
import Gallery from './Gallery.js';
import { Profile } from './Profile.js';

export default function App() {
  return (
    <div>
      <Profile />
      <Gallery />
    </div>
  );
}
```

```js src/Gallery.js
import { Profile } from './Profile.js';

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

```js src/Profile.js
export function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

ఇది డిఫాల్ట్ ఎక్స్‌పోర్ట్స్‌తో సమాధానం:

<Sandpack>

```js src/App.js
import Gallery from './Gallery.js';
import Profile from './Profile.js';

export default function App() {
  return (
    <div>
      <Profile />
      <Gallery />
    </div>
  );
}
```

```js src/Gallery.js
import Profile from './Profile.js';

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

```js src/Profile.js
export default function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

</Solution>

</Challenges>
