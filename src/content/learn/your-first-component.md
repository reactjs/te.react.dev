---
title: మీ మొదటి కంపోనెంట్
---

<Intro>

*కంపోనెంట్‌లు* అనేవి React యొక్క ప్రధాన కాన్సెప్ట్‌లలో ఒకటి. ఇవి యూజర్ ఇంటర్‌ఫేస్‌లు (UI) ని నిర్మించే పునాది, అందుకే React నేర్చుకునే జర్నీ ప్రారంభించడానికి ఇది ఉత్తమమైన ప్రదేశం!

</Intro>

<YouWillLearn>

* కంపోనెంట్ అంటే ఏమిటి
* React యాప్‌లో కంపోనెంట్‌లు ఏ పాత్ర పోషిస్తాయి
* మీ మొదటి React కంపోనెంట్ రాయడం ఎలా

</YouWillLearn>

## కంపోనెంట్‌లు: UI బిల్డింగ్ బ్లాక్స్ {/*components-ui-building-blocks*/}

Web లో, HTML దాని బిల్ట్-ఇన్ `<h1>` మరియు `<li>` వంటి ట్యాగ్‌ల సెట్‌తో రిచ్ స్ట్రక్చర్డ్ డాక్యుమెంట్‌లను రూపొందించడానికి అనుమతిస్తుంది:

```html
<article>
  <h1>My First Component</h1>
  <ol>
    <li>Components: UI Building Blocks</li>
    <li>Defining a Component</li>
    <li>Using a Component</li>
  </ol>
</article>
```

ఈ మార్కప్ ఈ ఆర్టికల్ ని రిప్రజెంట్ చేస్తుంది `<article>`, దాని హెడ్డింగ్ `<h1>`, మరియు టేబుల్ ఆఫ్ కంటెంట్‌ను `<ol>` రూపంలో ప్రదర్శిస్తుంది. ఇలాంటి మార్కప్, స్టైల్ కోసం CSS, మరియు ఇంటరాక్టివిటీ కోసం JavaScript కలిసి, Web లో మీరు చూస్తున్న ప్రతి సైడ్‌బార్, అవతార్, మోడల్, డ్రాప్‌డౌన్ — ప్రతి UI కంపోనెంట్ వెనుక కలిసి ఉంటాయి.

React మీ మార్కప్, CSS, మరియు JavaScript ను కస్టమ్ "కంపోనెంట్స్" గా కలిపే అవకాశాన్ని ఇస్తుంది, **మీ యాప్‌కు రీయూజబుల్ UI ఎలిమెంట్స్.** మీరు పై కోడ్‌ను `<TableOfContents />` కంపోనెంట్‌గా మార్చి ప్రతి పేజీలో కూడా రెండర్ చేయవచ్చు. అంతర్గతంగా, ఇది ఇంకా అదే HTML ట్యాగ్లను ఉపయోగిస్తుంది, ఉదాహరణకు `<article>`, `<h1>` మరియు తదితరాలు.

HTML ట్యాగ్‌లతో చేసినట్లుగా, మీరు కంపోనెంట్స్‌ని కలపడం, ఆర్డర్ చేయడం మరియు నెస్టింగ్ చేయడం ద్వారా పూర్తి పేజీలను డిజైన్ చేయవచ్చు. ఉదాహరణకు, మీరు చదివే డాక్యుమెంటేషన్ పేజీ React కంపోనెంట్స్‌తో తయారైంది:

```js
<PageLayout>
  <NavigationHeader>
    <SearchBar />
    <Link to="/docs">Docs</Link>
  </NavigationHeader>
  <Sidebar />
  <PageContent>
    <TableOfContents />
    <DocumentationText />
  </PageContent>
</PageLayout>
```

మీ ప్రాజెక్ట్ పెరుగుతున్న కొద్దీ, మీరు ఇప్పటికే రాసిన కంపోనెంట్లను రీయూజ్ చేయడం ద్వారా మీ డిజైన్లను రూపొందించవచ్చని గమనిస్తారు, తద్వారా మీ డెవలప్మెంట్ వేగవంతం అవుతుంది. మా పై టేబుల్ ఆఫ్ కంటెంట్‌ను ఏ స్క్రీన్‌లోనైనా `<TableOfContents />` ద్వారా చేర్చవచ్చు! మీరు React ఓపెన్ సోర్స్ కమ్యూనిటీ ద్వారా పంచబడిన వేలాది కంపోనెంట్లను ఉపయోగించి మీ ప్రాజెక్ట్‌ను ప్రారంభించవచ్చు, ఉదాహరణకు [Chakra UI](https://chakra-ui.com/) మరియు [Material UI](https://material-ui.com/).

## కంపోనెంట్‌ ను డిఫైన్ చేయడం {/*defining-a-component*/}

సాంప్రదాయంగా వెబ్ పేజీలను క్రియేట్ చేస్తున్నప్పుడు, వెబ్ డెవలపర్లు ముందుగా వారి కంటెంట్‌ను మార్కప్ చేసి, తరువాత కొంచెం JavaScript ని జోడించడం ద్వారా ఇంటరాక్షన్‌ను అందించేవారు. ఇది ఇంటరాక్షన్ ఒక అదనపు ఫీచర్ లాగా ఉన్నప్పుడు బాగా పనిచేసేది. కానీ ఇప్పుడు, ఇది చాలా సైట్లకు మరియు అన్ని యాప్‌లకు అవసరంగా మారింది. React ఇంటరాక్షన్‌ను మొదటి ప్రాధాన్యంగా ఉంచుతుంది, అయినప్పటికీ అదే టెక్నాలజీని ఉపయోగిస్తుంది: **React కాంపొనెంట్ అనేది JavaScript ఫంక్షన్, దీనిని మీరు _మార్కప్‌తో కలపవచ్చు_.** ఇది ఎలా కనిపిస్తుందో ఇక్కడ ఉంది (క్రింది ఉదాహరణను మీరు ఎడిట్ చేయవచ్చు):

<Sandpack>

```js
export default function Profile() {
  return (
    <img
      src="https://react.dev/images/docs/scientists/MK3eW3Am.jpg"
      alt="Katherine Johnson"
    />
  )
}
```

```css
img { height: 200px; }
```

</Sandpack>

ఇలా కాంపొనెంట్‌ను నిర్మించవచ్చు:

### స్టెప్ 1: కంపోనెంట్‌ను ఎక్స్‌పోర్ట్ చేయండి {/*step-1-export-the-component*/}

`export default` ప్రిఫిక్స్ ఒక [స్టాండర్డ్ JavaScript సింటాక్స్](https://developer.mozilla.org/docs/web/javascript/reference/statements/export) (React కి ప్రత్యేకం కాదు). ఇది మీరు ఒక ఫైల్‌లో మెయిన్ ఫంక్షన్‌ ని మార్క్ చేయడానికి అనుమతిస్తుంది, తద్వారా మీరు ఆ ఫంక్షన్‌ ని ఇతర ఫైళ్ల నుంచి ఇంపోర్ట్ చేసుకోవచ్చు. (కంపోనెంట్లను [ఇంపోర్ట్ మరియు ఎక్స్‌పోర్ట్ చేయడం](/learn/importing-and-exporting-components) గురించి మరింత తెలుసుకోండి!)

### స్టెప్ 2: ఫంక్షన్ ని డిఫైన్ చేయండి {/*step-2-define-the-function*/}

`function Profile() { }` తో మీరు `Profile` అనే పేరుతో ఒక JavaScript ఫంక్షన్ ని డిఫైన్ చేస్తారు.

<Pitfall>

React కంపోనెంట్లు సాధారణ JavaScript ఫంక్షన్‌లే, కానీ **వాటి పేర్లు పెద్ద అక్షరంతో ప్రారంభమవ్వాలి** లేకపోతే అవి పని చేయవు!

</Pitfall>

### స్టెప్ 3: మార్కప్ జోడించండి {/*step-3-add-markup*/}

కంపోనెంట్ `src` మరియు `alt` అట్రిబ్యూట్లతో కూడిన `<img />` ట్యాగ్‌ను రిటర్న్ చేస్తుంది. `<img />` ను HTML లాగా రాస్తారు, కానీ ఇది వాస్తవానికి JavaScript లో ఉండే కోడ్! ఈ సింటాక్స్‌ను [JSX](/learn/writing-markup-with-jsx) అని పిలుస్తారు, మరియు ఇది JavaScript లో మార్కప్‌ను ఎంబెడ్ చేయటానికి అనుమతిస్తుంది.

రిటర్న్ స్టేట్మెంట్‌ను ఈ కంపోనెంట్‌లోని విధంగా ఒకే లైనులో రాయవచ్చు:

```js
return <img src="https://react.dev/images/docs/scientists/MK3eW3As.jpg" alt="Katherine Johnson" />;
```

మీ మార్కప్ `return` కీవర్డ్‌తో ఒకే లైన్‌లో లేకపోతే, మీరు దాన్ని ఒక జంట పేరెంటీసిస్‌లో చుట్టాలి:

```js
return (
  <div>
    <img src="https://react.dev/images/docs/scientists/MK3eW3As.jpg" alt="Katherine Johnson" />
  </div>
);
```

<Pitfall>

పేరెంటీసిస్ లేకుండా, `return` తర్వాతి లైన్లలో ఉన్న ఎలాంటి కోడ్ కూడా [గమనించబడదు](https://stackoverflow.com/questions/2846283/what-are-the-rules-for-javascripts-automatic-semicolon-insertion-asi)!

</Pitfall>

## ఒక కంపోనెంట్ ను ఉపయోగించడం {/*using-a-component*/}

ఇప్పుడు మీరు మీ `Profile` కంపోనెంట్‌ను డిఫైన్ చేసిన తర్వాత, మీరు దీన్ని ఇతర కంపోనెంట్లలో నెస్టు చేయవచ్చు. ఉదాహరణకు, మీరు అనేక `Profile` కంపోనెంట్లను ఉపయోగించే `Gallery` కంపోనెంట్‌ను ఎక్స్‌పోర్ట్ చేయవచ్చు:

<Sandpack>

```js
function Profile() {
  return (
    <img
      src="https://react.dev/images/docs/scientists/MK3eW3As.jpg"
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

### బ్రౌజర్ ఏమి చూస్తుంది {/*what-the-browser-sees*/}

కేస్‌లో ఉన్న తేడాను గమనించండి:

* `<section>` ఇది చిన్న అక్షరాలలో ఉంది, కాబట్టి React కు తెలుసు మనం HTML ట్యాగ్‌ను సూచిస్తున్నాము.
* `<Profile />` ఇది పెద్ద `P` తో ప్రారంభమవుతుంది, కాబట్టి React కు తెలుసు మనం `Profile` అనే కాంపొనెంట్‌ను ఉపయోగించాలనుకుంటున్నాము.

మరియు `Profile` లో ఇంకా HTML ఉంది: `<img />`. చివరికి, బ్రౌజర్ ఇది చూస్తుంది:

```html
<section>
  <h1>Amazing scientists</h1>
  <img src="https://react.dev/images/docs/scientists/MK3eW3As.jpg" alt="Katherine Johnson" />
  <img src="https://react.dev/images/docs/scientists/MK3eW3As.jpg" alt="Katherine Johnson" />
  <img src="https://react.dev/images/docs/scientists/MK3eW3As.jpg" alt="Katherine Johnson" />
</section>
```

### కంపోనెంట్లను నెస్టింగ్ మరియు ఆర్గనైజ్ చేయడం {/*nesting-and-organizing-components*/}

కంపోనెంట్లు సాధారణ JavaScript ఫంక్షన్లు, కాబట్టి మీరు ఒకే ఫైల్‌లో అనేక కంపోనెంట్లను ఉంచవచ్చు. కాంపొనెంట్‌లు చిన్నవిగా లేదా పరస్పరంగా బలంగా సంబంధం ఉన్నప్పుడు ఇది అనుకూలంగా ఉంటుంది. ఈ ఫైలు చాలా నిండి పోయినప్పుడు, మీరు ఎప్పుడైనా `Profile` కంపోనెంట్‌ను ప్రత్యేకమైన ఫైల్‌కు తరలించవచ్చు. మీరు ఈ విధానం గురించి త్వరలో [ఇంపోర్ట్స్ పేజీలో](/learn/importing-and-exporting-components) నేర్చుకుంటారు.

కారణంగా, `Profile` కంపోనెంట్స్ `Gallery` లో రేండర్ అవుతున్నాయి—చెప్పాలంటే, అనేకసార్లు!—కాబట్టి మనం చెప్పవచ్చు `Gallery` అనేది ఒక **పేరెంట్ కంపోనెంట్**, మరియు ప్రతి `Profile` ను "చైల్డ్" గా రేండర్ చేస్తుంది. ఇది React యొక్క మ్యాజిక్ భాగం: మీరు ఒక కంపోనెంట్ని ఒకసారి డిఫైన్ చేసి, అప్పుడు దాన్ని మీరు ఇష్టపడే ఎన్ని ప్రదేశాల్లోనూ, ఎన్ని సార్లు అయినా ఉపయోగించవచ్చు.

<Pitfall>

కంపోనెంట్లు మరొక కంపోనెంట్లను రేండర్ చేయవచ్చు, కానీ **మీరు వాటి డిఫినిషన్స్‌ను ఎప్పుడూ నెస్ట్ చేయకూడదు:**

```js {2-5}
export default function Gallery() {
  // 🔴 Never define a component inside another component!
  function Profile() {
    // ...
  }
  // ...
}
```

పై కోడ్ [చాలా మెల్లగా పనిచేస్తుంది మరియు బగ్స్‌ను కలిగిస్తుంది.](/learn/preserving-and-resetting-state#different-components-at-the-same-position-reset-state) దాని స్థానంలో, ప్రతి కంపోనెంట్‌ను టాప్ లెవెల్‌లో నిర్వచించండి:

```js {5-8}
export default function Gallery() {
  // ...
}

// ✅ Declare components at the top level
function Profile() {
  // ...
}
```

ఒక చైల్డ్ కంపోనెంట్కు ఒక ప్యారెంట్ నుండి డేటా అవసరమైతే, [props ద్వారా పంపండి](/learn/passing-props-to-a-component) డిఫినిషన్స్‌ను నెస్ట్ చేయడం కాకుండా.

</Pitfall>

<DeepDive>

#### కంపోనెంట్లు ప్రారంభం నుంచి చివరి వరకు {/*components-all-the-way-down*/}

మీ React అప్లికేషన్ ఒక "రూట్" కంపోనెంట్‌తో ప్రారంభం అవుతుంది. సాధారణంగా, మీరు కొత్త ప్రాజెక్ట్ ప్రారంభించినప్పుడు ఇది ఆటోమాటిక్‌గా సృష్టించబడుతుంది. ఉదాహరణకు, మీరు [CodeSandbox](https://codesandbox.io/) లేదా [Next.js](https://nextjs.org/) ఫ్రేమ్‌వర్క్‌ను ఉపయోగిస్తే, రూట్ కంపోనెంట్ `pages/index.js` లో డిఫైన్ చేయబడుతుంది. ఈ ఉదాహరణల్లో, మీరు రూట్ కంపోనెంట్లను ఎక్స్‌పోర్ట్ చేస్తున్నారు.

చాలా వరకు React యాప్స్ కంపోనెంట్స్‌ను ప్రారంభం నుంచి చివరి వరకు ఉపయోగిస్తాయి. అంటే, మీరు కేవలం రీయూజబుల్ భాగాలు, ఉదాహరణకు బటన్‌లతో మాత్రమే కంపోనెంట్స్‌ను ఉపయోగించరు, కానీ పెద్ద భాగాలు, ఉదాహరణకు సైడ్‌బార్లు, లిస్ట్లు మరియు చివరగా పూర్తి పేజీలు కూడా! కంపోనెంట్స్ UI కోడ్ మరియు మార్కప్‌ ను ఆర్గనైజ్ చేయడానికి చాలా ఉపయోగకరమైన మార్గం, కొన్నిటిని ఒకసారి మాత్రమే ఉపయోగించినా కూడా.

[React ఆధారిత ఫ్రేమ్‌వర్క్‌లు](/learn/creating-a-react-app) ఈ దశను మరింత ముందుకు తీసుకెళ్తుంది. ఖాళీ HTML ఫైల్ ఉపయోగించి React‌ తో JavaScript ద్వారా పేజీని "నియంత్రించేందుకు" అవకాశం ఇవ్వడం కంటే బదులు, React కంపోనెంట్ల నుండి HTML‌ ను ఆటోమేటిక్‌గా సృష్టించవచ్చు.  ఇది JavaScript కోడ్ లోడ్ అవ్వడానికి ముందే మీ యాప్ కొన్ని కంటెంట్‌ను ప్రదర్శించేందుకు అనుమతిస్తుంది.

అయితే, అనేక వెబ్‌సైట్లు React ని కేవలం [కొన్ని HTML పేజీలకు ఇంటరాక్టివిటీ జోడించడానికి](/learn/add-react-to-an-existing-project#using-react-for-a-part-of-your-existing-page) మాత్రమే ఉపయోగిస్తాయి. అవి పేజీ మొత్తం కోసం ఒకే ఒక రూట్ కాంపొనెంట్ యొక్క స్థానంలో అనేక రూట్ కాంపొనెంట్లను కలిగి ఉంటాయి. మీరు ఎంత React ఉపయోగించాలనుకుంటే అంత లేదా కొంత React ఉపయోగించవచ్చు.

</DeepDive>

<Recap>

మీరు React యొక్క మొదటి పరిచయాన్ని పొందారు! కొన్ని ముఖ్యమైన పాయింట్లను తిరిగి గుర్తు చేసుకుందాం.

* React మీరు **మీ యాప్ కోసం రీయూజబుల్ UI ఎలిమెంట్స్** అయిన కంపోనెంట్లను సృష్టించడానికి అనుమతిస్తుంది.
* React యాప్‌లో ప్రతి UI భాగం ఒక కంపోనెంట్.
* React కంపోనెంట్లు సాధారణ JavaScript ఫంక్షన్లు అయినప్పటికీ:

  1. వాటి పేర్లు ఎల్లప్పుడూ పెద్ద అక్షరంతో ప్రారంభం అవుతాయి.
  2. అవి JSX మార్కప్‌ను return చేస్తాయి.

</Recap>



<Challenges>

#### కంపోనెంట్‌ను ఎక్స్‌పోర్ట్ చేయండి {/*export-the-component*/}

ఈ శాండ్‌బాక్స్ పని చేయడం లేదు, ఎందుకంటే రూట్ కంపోనెంట్ ఎక్స్‌పోర్ట్ చేయబడలేదు:

<Sandpack>

```js
function Profile() {
  return (
    <img
      src="https://react.dev/images/docs/scientists/lICfvbD.jpg"
      alt="Aklilu Lemma"
    />
  );
}
```

```css
img { height: 181px; }
```

</Sandpack>

పరిష్కారాన్ని చూడటానికి ముందు దానిని మీరు స్వయంగా సరిచేయడానికి ప్రయత్నించండి!

<Solution>

ఫంక్షన్ డెఫినేషన్ కి ముందు `export default` ని జోడించండి ఇలా:

<Sandpack>

```js
export default function Profile() {
  return (
    <img
      src="https://react.dev/images/docs/scientists/lICfvbD.jpg"
      alt="Aklilu Lemma"
    />
  );
}
```

```css
img { height: 181px; }
```

</Sandpack>

మీరు ఈ ఉదాహరణను సరిచేయడానికి కేవలం `export` వ్రాయడం ఎందుకు సరిపోదు అని ఆలోచిస్తున్నట్లయితే. `export` మరియు `export default` మధ్య తేడా తెలుసుకోడానికి [కంపోనెంట్లను ఇంపోర్ట్ మరియు ఎక్స్‌పోర్ట్ చేసుకోవడం](/learn/importing-and-exporting-components) గురించి చూడండి.

</Solution>

#### return స్టేట్‌మెంట్‌ ని సరిచేయండి {/*fix-the-return-statement*/}

ఈ `return` స్టేట్‌మెంట్‌లో ఏదో సరిగ్గా లేదు. మీరు దీన్ని సరిచేయగలరా?

<Hint>

మీరు దీన్ని సరి చేసేటప్పుడు "Unexpected token" ఎర్రర్ వస్తే, దయచేసి పరిక్షించండి, సెమికోలన్ `return ( )` ముగిసిన తరువాత రావాలి. సెమికోలన్‌ను `return ( )` లోపల ఉంచితే ఎర్రర్ వస్తుంది.

</Hint>


<Sandpack>

```js
export default function Profile() {
  return
    <img src="https://react.dev/images/docs/scientists/jA8hHMpm.jpg" alt="Katsuko Saruhashi" />;
}
```

```css
img { height: 180px; }
```

</Sandpack>

<Solution>

మీరు ఈ కంపోనెంట్‌ని సరి చేసేందుకు, return స్టేట్మెంట్‌ను ఒకే లైన్‌లో కింద చూపించినట్లుగా మార్చవచ్చు:

<Sandpack>

```js
export default function Profile() {
  return <img src="https://react.dev/images/docs/scientists/jA8hHMpm.jpg" alt="Katsuko Saruhashi" />;
}
```

```css
img { height: 180px; }
```

</Sandpack>

లేదా `return` తరువాత వెంటనే తెరవబడే పేరెంటీసిస్ లో JSX మార్కప్‌ను చుట్టి రాయడం ద్వారా:

<Sandpack>

```js
export default function Profile() {
  return (
    <img
      src="https://react.dev/images/docs/scientists/jA8hHMpm.jpg"
      alt="Katsuko Saruhashi"
    />
  );
}
```

```css
img { height: 180px; }
```

</Sandpack>

</Solution>

#### పొరపాటును కనుగొనండి {/*spot-the-mistake*/}

`Profile` కంపోనెంట్ ఎలా డిక్లేర్ చేయబడిందో మరియు ఉపయోగించబడిందో ఒకసారి పరిశీలించండి. మీరు తప్పు ఎక్కడ ఉంది అన్నదాన్ని గుర్తించగలరా? (React ఎలా కంపోనెంట్లను సాధారణ HTML ట్యాగుల నుండి వేరు చేస్తుందో గుర్తు తెచ్చుకోండి!)

<Sandpack>

```js
function profile() {
  return (
    <img
      src="https://react.dev/images/docs/scientists/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <profile />
      <profile />
      <profile />
    </section>
  );
}
```

```css
img { margin: 0 10px 10px 0; height: 90px; }
```

</Sandpack>

<Solution>

React కంపోనెంట్ పేర్లు పెద్ద అక్షరంతో ప్రారంభించాలి.

`function profile()` ని `function Profile()` గా మార్చండి, మరియు ఆపై ప్రతి `<profile />` ని `<Profile />` గా మార్చండి:

<Sandpack>

```js
function Profile() {
  return (
    <img
      src="https://react.dev/images/docs/scientists/QIrZWGIs.jpg"
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
img { margin: 0 10px 10px 0; }
```

</Sandpack>

</Solution>

#### మీ స్వంత కంపోనెంట్ {/*your-own-component*/}

మీరు ఒక కొత్త కంపోనెంట్‌ని ప్రారంభించండి. మీరు దానికి ఏదైనా సరైన పేరు ఇవ్వవచ్చు మరియు ఏదైనా మార్కప్‌ని return చేయవచ్చు. మీకు ఆలోచనలేమైనా లేకపోతే, మీరు `Congratulations` కంపోనెంట్‌ను రాయవచ్చు, ఇది `<h1>Good job!</h1>` ని చూపిస్తుంది. దాన్ని ఎక్స్‌పోర్ట్ చేయడం మర్చిపోకండి!

<Sandpack>

```js
// Write your component below!

```

</Sandpack>

<Solution>

<Sandpack>

```js
export default function Congratulations() {
  return (
    <h1>Good job!</h1>
  );
}
```

</Sandpack>

</Solution>

</Challenges>
