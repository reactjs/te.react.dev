---
title: JSX తో మార్కప్ రాయడం
---

<Intro>

*JSX* అనేది JavaScript కోసం ఒక సింటాక్స్ ఎక్స్‌టెన్షన్. ఇది JavaScript ఫైల్‌లో HTML లాంటి మార్కప్ రాయడానికి అనుమతిస్తుంది. కంపోనెంట్లను రాయడానికి ఇతర మార్గాలు ఉన్నప్పటికీ, చాలా React డెవలపర్లు JSX యొక్క సౌకర్యాన్ని ఇష్టపడతారు మరియు చాలా కోడ్‌బేస్‌లు దీనిని ఉపయోగిస్తాయి.

</Intro>

<YouWillLearn>

* React మార్కప్‌ను రెండరింగ్ లాజిక్‌తో ఎందుకు కలుపుతుంది
* JSX HTML కి ఎలా భిన్నంగా ఉంటుంది
* JSX ద్వారా సమాచారం ఎలా ప్రదర్శించాలి

</YouWillLearn>

## JSX: మార్కప్‌ను JavaScript లో ఉంచడం {/*jsx-putting-markup-into-javascript*/}

Web అనేది HTML, CSS, మరియు JavaScript పై ఆధారపడి నిర్మించబడింది. చాలా సంవత్సరాలుగా, వెబ్ డెవలపర్లు కంటెంట్‌ను HTML లో, డిజైన్‌ను CSS లో, మరియు లాజిక్‌ను JavaScript లో విడిగా ఉంచేవారు—ఇప్పటికీ వేరే ఫైళ్లలో! కంటెంట్ HTML లో మార్కప్ చేయబడేది, ఆ పేజీ యొక్క లాజిక్ మాత్రం JavaScript లో వేరుగా ఉండేది:

<DiagramGroup>

<Diagram name="writing_jsx_html" height={237} width={325} alt="HTML markup with purple background and a div with two child tags: p and form. ">

HTML

</Diagram>

<Diagram name="writing_jsx_js" height={237} width={325} alt="Three JavaScript handlers with yellow background: onSubmit, onLogin, and onClick.">

JavaScript

</Diagram>

</DiagramGroup>

కానీ Web మరింత ఇంటరాక్టివ్‌గా మారుతున్న కొద్దీ, లాజిక్ ఎక్కువగా కంటెంట్‌ను నిర్ణయించింది. JavaScript HTML ని నియంత్రించేది! అందుకే **React లో, రెండరింగ్ లాజిక్ మరియు మార్కప్ కంపోనెంట్లలో ఒకే చోట ఉంటాయి.**

<DiagramGroup>

<Diagram name="writing_jsx_sidebar" height={330} width={325} alt="React component with HTML and JavaScript from previous examples mixed. Function name is Sidebar which calls the function isLoggedIn, highlighted in yellow. Nested inside the function highlighted in purple is the p tag from before, and a Form tag referencing the component shown in the next diagram.">

`Sidebar.js` React కంపోనెంట్

</Diagram>

<Diagram name="writing_jsx_form" height={330} width={325} alt="React component with HTML and JavaScript from previous examples mixed. Function name is Form containing two handlers onClick and onSubmit highlighted in yellow. Following the handlers is HTML highlighted in purple. The HTML contains a form element with a nested input element, each with an onClick prop.">

`Form.js` React కంపోనెంట్

</Diagram>

</DiagramGroup>

బటన్ యొక్క రెండరింగ్ లాజిక్ మరియు మార్కప్‌ను కలిపి ఉంచడం వల్ల, ప్రతిసారి మార్పులు చేసినప్పుడు అవి ఒకే సమన్వయంతో ఉండేలా చేస్తుంది. మరోవైపు, బటన్ యొక్క మార్కప్ మరియు సైడ్బార్ యొక్క మార్కప్ వంటి సంబంధం లేని వివరాలు ఒకదానితో ఒకటి ప్రత్యేకంగా ఉంచబడతాయి, దీనివల్ల వాటిలో ఏదైనా స్వతంత్రంగా మార్చడం మరింత సురక్షితంగా ఉంటుంది.

ప్రతి React కంపోనెంట్ అనేది JavaScript ఫంక్షన్, ఇది React బ్రౌజర్‌లో రెండర్ చేసే కొంత మార్కప్‌ను కలిగి ఉండవచ్చు. React కంపోనెంట్‌లు ఆ మార్కప్‌ను ప్రదర్శించడానికి JSX అనే సింటాక్స్ ఎక్స్‌టెన్షన్ ఉపయోగిస్తాయి. JSX HTML లాంటిదిగా కనిపిస్తుంది, కానీ ఇది కొంచెం కఠినంగా ఉంటుంది మరియు డైనమిక్ సమాచారాన్ని ప్రదర్శించగలదు. దీనిని అర్థం చేసుకోవడానికి ఉత్తమమైన మార్గం, కొంత HTML మార్కప్‌ను JSX మార్కప్‌లోకి మార్చడం.

<Note>

JSX మరియు React రెండు వేర్వేరు విషయాలు. వీటిని తరచుగా కలిపి ఉపయోగిస్తారు, కానీ మీరు [వాటిని స్వతంత్రంగా ఉపయోగించవచ్చు](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html#whats-a-jsx-transform). JSX అనేది ఒక సింటాక్స్ ఎక్స్‌టెన్షన్ కాగా, React అనేది ఒక JavaScript లైబ్రరీ.

</Note>

## HTML ని JSX గా మార్చడం {/*converting-html-to-jsx*/}

మీ దగ్గర కొంత (పూర్తిగా సరైన) HTML ఉందని అనుకుందాం:

```html
<h1>Hedy Lamarr's Todos</h1>
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg" 
  alt="Hedy Lamarr" 
  class="photo"
>
<ul>
    <li>Invent new traffic lights
    <li>Rehearse a movie scene
    <li>Improve the spectrum technology
</ul>
```

మరియు మీరు దానిని మీ కంపోనెంట్‌లో పెట్టాలనుకుంటున్నట్లయితే:

```js
export default function TodoList() {
  return (
    // ???
  )
}
```

మీరు కాపీ చేసి అలాగే పేస్ట్ చేస్తే, ఇది పని చేయదు:


<Sandpack>

```js
export default function TodoList() {
  return (
    // This doesn't quite work!
    <h1>Hedy Lamarr's Todos</h1>
    <img 
      src="https://i.imgur.com/yXOvdOSs.jpg" 
      alt="Hedy Lamarr" 
      class="photo"
    >
    <ul>
      <li>Invent new traffic lights
      <li>Rehearse a movie scene
      <li>Improve the spectrum technology
    </ul>
  );
}
```

```css
img { height: 90px }
```

</Sandpack>

ఇది ఎందుకంటే JSX HTML కంటే కఠినమైనది మరియు దాని కోసం కొన్ని అదనపు నియమాలు ఉన్నాయి! మీరు పై ఎర్రర్ మెసేజ్‌లను చదవితే, అవి మార్కప్‌ని సరిచేయడంలో మీకు మార్గనిర్దేశం చేస్తాయి, లేదా మీరు కింద ఉన్న గైడ్‌ను అనుసరించవచ్చు.

<Note>

చాలా సమయాల్లో, React యొక్క ఆన్-స్క్రీన్ ఎర్రర్ మెసేజ్‌లు సమస్య ఎక్కడ ఉందో కనుగొనడంలో మీకు సహాయపడతాయి. మీరు చిక్కులో పడితే, వాటిని చదవండి!

</Note>

## JSX యొక్క నియమాలు {/*the-rules-of-jsx*/}

### 1. ఒకే రూట్ ఎలిమెంట్‌ని return చేయండి {/*1-return-a-single-root-element*/}

కంపోనెంట్ల నుంచి అనేక ఎలిమెంట్స్‌ని return చేయాలంటే, **వాటిని ఒకే పేరెంట్ ట్యాగ్‌తో చుట్టండి.**

ఉదాహరణకు, మీరు `<div>`ని ఉపయోగించవచ్చు:

```js {1,11}
<div>
  <h1>Hedy Lamarr's Todos</h1>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
  >
  <ul>
    ...
  </ul>
</div>
```


మీరు మీ మార్కప్‌కి అదనపు `<div>` జోడించకూడదనుకుంటే, మీరు బదులుగా `<>` మరియు `</>` వ్రాయవచ్చు:

```js {1,11}
<>
  <h1>Hedy Lamarr's Todos</h1>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
  >
  <ul>
    ...
  </ul>
</>
```

ఈ ఖాళీ ట్యాగ్‌ని *[Fragment](/reference/react/Fragment)* అని అంటారు. Fragments బ్రౌజర్ HTML ట్రీలో ఎలాంటి జాడను వదలకుండా విషయాలను సమూహపరచడానికి మిమ్మల్ని అనుమతిస్తాయి.

<DeepDive>

#### ఎందుకు మల్టిపుల్ JSX ట్యాగ్‌లను ర్యాప్ చేయాలి? {/*why-do-multiple-jsx-tags-need-to-be-wrapped*/}

JSX HTML లాగా కనిపిస్తుంది, కానీ లోపలి భాగంలో ఇది సాధారణ JavaScript ఆబ్జెక్టులుగా మార్చబడుతుంది. మీరు ఒక ఫంక్షన్ నుండి రెండు ఆబ్జెక్టులను తిరిగి ఇచ్చే అవకాశం లేదు, అవి ఒక array లో ర్యాప్ చేయాల్సి ఉంటుంది. ఇదే కారణంగా, మీరు రెండు JSX ట్యాగ్‌లను కూడా మరో ట్యాగ్ లేదా fragment లో ర్యాప్ చేయకుండా తిరిగి ఇవ్వలేరు.

</DeepDive>

### 2. అన్ని ట్యాగ్‌లను మూసివేయండి {/*2-close-all-the-tags*/}

JSX లో ట్యాగ్‌లను స్పష్టంగా మూసివేయాల్సి ఉంటుంది: స్వయంగా మూసే ట్యాగ్‌లాంటి `<img>` ను `<img />` గా మార్చాలి, మరియు చుట్టుకొలత ట్యాగ్‌లాంటి `<li>oranges` ను `<li>oranges</li>` అని రాయాలి.

ఇది Hedy Lamarr యొక్క చిత్రమూ, లిస్ట్ అంశాలు ఎలా మూసివేయబడ్డాయో చూడండి:

```js {2-6,8-10}
<>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
   />
  <ul>
    <li>Invent new traffic lights</li>
    <li>Rehearse a movie scene</li>
    <li>Improve the spectrum technology</li>
  </ul>
</>
```

### 3. camelCase <s>అన్ని</s> చాలా విషయాలు! {/*3-camelcase-salls-most-of-the-things*/}

JSX JavaScript గా మారుతుంది మరియు JSX లో రాసిన అట్రిబ్యూట్లు JavaScript ఆబ్జెక్టుల key లు అవుతాయి. మీ స్వంత కాంపోనెంట్లలో, మీరు తరచుగా ఆ అట్రిబ్యూట్లను వేరియబుల్స్‌లో చదవాలనుకుంటారు. కానీ JavaScript వేరియబుల్ పేర్లపై కొన్ని పరిమితులు ఉన్నాయి. ఉదాహరణకు, వాటి పేర్లలో డాష్‌లు ఉండకూడదు లేదా `class` వంటి రిజర్వ్ చేసిన పదాలు ఉండకూడదు.

అందుకే React లో, చాలా HTML మరియు SVG అట్రిబ్యూట్లు camelCase లో రాయబడతాయి. ఉదాహరణకు, `stroke-width` బదులుగా మీరు `strokeWidth` ఉపయోగిస్తారు. `class` అనేది రిజర్వ్ చేసిన పదం కావడం వలన, React లో మీరు `className` అని రాస్తారు, ఇది [అనుకూల DOM ప్రాపర్టీ](https://developer.mozilla.org/en-US/docs/Web/API/Element/className) ఆధారంగా ఉంటుంది:

```js {4}
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg" 
  alt="Hedy Lamarr" 
  className="photo"
/>
```

మీరు [ఈ అన్ని అట్రిబ్యూట్లను DOM కంపోనెంట్ ప్రాపర్టీలు యొక్క లిస్ట్‌లో కనుగొనవచ్చు](/reference/react-dom/components/common). మీరు వాటిలో ఒకటి తప్పు చేసినా, చింతించకండి—React ఒక సందేశాన్ని ప్రింట్ చేస్తుంది, దాని పరిష్కారం కోసం [బ్రౌజర్ కన్సోల్](https://developer.mozilla.org/docs/Tools/Browser_Console) లో చూడండి.

<Pitfall>

చరిత్రాత్మక కారణాల వల్ల, [`aria-*`](https://developer.mozilla.org/docs/Web/Accessibility/ARIA) మరియు [`data-*`](https://developer.mozilla.org/docs/Learn/HTML/Howto/Use_data_attributes) అట్రిబ్యూట్లు HTML లో డాష్‌లతో రాయబడతాయి.

</Pitfall>

### ప్రో-టిప్: JSX కన్వర్టర్‌ను ఉపయోగించండి {/*pro-tip-use-a-jsx-converter*/}

ఇప్పటికే ఉన్న మార్కప్‌లో ఈ అట్రిబ్యూట్లను అన్నింటినీ మార్చడం చాలా శ్రమతో కూడుకున్నది! మీ ప్రస్తుత HTML మరియు SVGని JSXకి అనువదించడానికి [కన్‌వర్టర్](https://transform.tools/html-to-jsx) ని ఉపయోగించమని మేము సిఫార్సు చేస్తున్నాము. కన్వర్టర్లు ప్రాక్టికల్‌గా చాలా ఉపయోగకరంగా ఉంటాయి, కానీ మీరు సరిగ్గా ఏం జరుగుతుందో అర్థం చేసుకోవడం ఇంకా విలువైనది, తద్వారా మీరు సొంతంగా JSX సౌకర్యంగా రాయగలుగుతారు.

ఇది మీ చివరి ఫలితం:

<Sandpack>

```js
export default function TodoList() {
  return (
    <>
      <h1>Hedy Lamarr's Todos</h1>
      <img 
        src="https://i.imgur.com/yXOvdOSs.jpg" 
        alt="Hedy Lamarr" 
        className="photo" 
      />
      <ul>
        <li>Invent new traffic lights</li>
        <li>Rehearse a movie scene</li>
        <li>Improve the spectrum technology</li>
      </ul>
    </>
  );
}
```

```css
img { height: 90px }
```

</Sandpack>

<Recap>

ఇప్పుడు మీరు JSX ఎందుకు ఉన్నదీ, కంపోనెంట్లలో దాన్ని ఎలా ఉపయోగించాలో తెలుసుకున్నారు:

* React కంపోనెంట్లు రెండరింగ్ లాజిక్ మరియు మార్కప్‌ను ఒకే చోట గ్రూప్ చేస్తాయి, ఎందుకంటే అవి పరస్పర సంబంధితమైనవి.
* JSX HTML లాగా ఉంటుంది, కానీ కొన్ని తేడాలు ఉన్నాయి. అవసరమైతే మీరు [కన్‌వర్టర్](https://transform.tools/html-to-jsx) ను ఉపయోగించవచ్చు.
* ఎర్రర్ మెసేజ్‌లు మీ మార్కప్‌ను సరిచేయడానికి సరైన దిశను చూపిస్తాయి.

</Recap>



<Challenges>

#### కొంత HTML ని JSX గా మార్చండి {/*convert-some-html-to-jsx*/}

ఈ HTML ను ఒక కంపోనెంట్‌లో పెట్టారు, కానీ ఇది సరైన JSX కాదు. దీన్ని సరిచేయండి:

<Sandpack>

```js
export default function Bio() {
  return (
    <div class="intro">
      <h1>Welcome to my website!</h1>
    </div>
    <p class="summary">
      You can find my thoughts here.
      <br><br>
      <b>And <i>pictures</b></i> of scientists!
    </p>
  );
}
```

```css
.intro {
  background-image: linear-gradient(to left, violet, indigo, blue, green, yellow, orange, red);
  background-clip: text;
  color: transparent;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.summary {
  padding: 20px;
  border: 10px solid gold;
}
```

</Sandpack>

దీనిని స్వయంగా చేయాలా లేదా కన్వర్టర్‌ను ఉపయోగించాలా అనేది మీ ఇష్టంపై ఆధారపడి ఉంటుంది!

<Solution>

<Sandpack>

```js
export default function Bio() {
  return (
    <div>
      <div className="intro">
        <h1>Welcome to my website!</h1>
      </div>
      <p className="summary">
        You can find my thoughts here.
        <br /><br />
        <b>And <i>pictures</i></b> of scientists!
      </p>
    </div>
  );
}
```

```css
.intro {
  background-image: linear-gradient(to left, violet, indigo, blue, green, yellow, orange, red);
  background-clip: text;
  color: transparent;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.summary {
  padding: 20px;
  border: 10px solid gold;
}
```

</Sandpack>

</Solution>

</Challenges>
