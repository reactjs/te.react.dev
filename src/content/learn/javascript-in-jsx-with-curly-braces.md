---
title: JSX లో కర్లీ బ్రేసెస్‌తో JavaScript
---

<Intro>

JSX మీకు JavaScript ఫైల్ లో HTML లాంటి మార్కప్ రాయడానికి అనుమతిస్తుంది, ఇది రెండరింగ్ లాజిక్ మరియు కంటెంట్‌ను ఒకే చోట ఉంచుతుంది. కొన్ని సందర్భాలలో, మీరు ఆ మార్కప్ లో కొంచెం JavaScript లాజిక్ లేదా డైనమిక్ ప్రాపర్టీని చేర్చాలనుకుంటారు. ఈ పరిస్థితిలో, మీరు JSX లో కర్లీ బ్రేసెస్‌ను ఉపయోగించి JavaScript కి ఒక విండో తెరవచ్చు.

</Intro>

<YouWillLearn>

* కోట్స్‌ తో strings ను ఎలా పాస్ చేయాలి
* JavaScript వేరియబుల్‌ను JSX లో కర్లీ బ్రేసెస్‌తో ఎలా రిఫరెన్స్ చేయాలి
* JavaScript ఫంక్షన్‌ను JSX లో కర్లీ బ్రేసెస్‌తో ఎలా కాల్ చేయాలి
* JavaScript ఆబ్జెక్ట్‌ను JSX లో కర్లీ బ్రేసెస్‌తో ఎలా ఉపయోగించాలి

</YouWillLearn>

## కోట్స్‌ తో strings ను పాస్ చేయడం {/*passing-strings-with-quotes*/}

మీరు JSX కు string అట్రిబ్యూట్‌ను పాస్ చేయాలనుకుంటే, మీరు దాన్ని సింగిల్ లేదా డబుల్ కోట్స్‌లో ఉంచాలి:

<Sandpack>

```js
export default function Avatar() {
  return (
    <img
      className="avatar"
      src="https://i.imgur.com/7vQD0fPs.jpg"
      alt="Gregorio Y. Zara"
    />
  );
}
```

```css
.avatar { border-radius: 50%; height: 90px; }
```

</Sandpack>

ఇక్కడ, `"https://i.imgur.com/7vQD0fPs.jpg"` మరియు `"Gregorio Y. Zara"` strings గా పాస్ అవుతున్నాయి.

కానీ మీరు డైనమిక్‌గా `src` లేదా `alt` టెక్ట్స్ ను స్పెసిఫై చేయాలనుకుంటే? మీరు **JavaScript నుండి వాల్యూలను ఉపయోగించడానికి `"` మరియు `"` ను `{` మరియు `}` తో మార్చవచ్చు**:

<Sandpack>

```js
export default function Avatar() {
  const avatar = 'https://i.imgur.com/7vQD0fPs.jpg';
  const description = 'Gregorio Y. Zara';
  return (
    <img
      className="avatar"
      src={avatar}
      alt={description}
    />
  );
}
```

```css
.avatar { border-radius: 50%; height: 90px; }
```

</Sandpack>

`className="avatar"` మరియు `src={avatar}` మధ్య తేడాని గమనించండి. `"avatar"` అనేది CSS class పేరు, ఇది చిత్రాన్ని రౌండ్ చేయడానికి ఉపయోగపడుతుంది, కానీ `src={avatar}` అనేది JavaScript వేరియబుల్ `avatar` యొక్క వాల్యూను చదువుతుంది. ఇది ఎందుకంటే కర్లీ బ్రేసెస్ అనేవి JSX లో JavaScript తో పని చేయడాన్ని అనుమతిస్తాయి!

## కర్లీ బ్రేసెస్ ఉపయోగించడం: JavaScript ప్రపంచంలోకి ఒక విండో {/*using-curly-braces-a-window-into-the-javascript-world*/}

JSX అనేది JavaScript రాయడానికి ఒక ప్రత్యేకమైన విధానం. అంటే, మీరు అందులో JavaScript ఉపయోగించవచ్చు—కర్లీ బ్రేసెస్ `{ }` తో. క్రింద ఇచ్చిన ఉదాహరణలో, మొదటా శాస్త్రవేత్త పేరు `name` గా డిక్లేర్ చేయబడింది, మరియు ఆ తరువాత దాన్ని కర్లీ బ్రేసెస్‌లో `<h1>` లో ఎంబెడ్ చేయబడింది:

<Sandpack>

```js
export default function TodoList() {
  const name = 'Gregorio Y. Zara';
  return (
    <h1>{name}'s To Do List</h1>
  );
}
```

</Sandpack>

`name` వాల్యూను `'Gregorio Y. Zara'` నుండి `'Hedy Lamarr'` గా మార్చే ప్రయత్నం చేయండి. లిస్ట్ టైటిల్ ఎలా మారుతుందో చూడండి?

ప్రతి JavaScript ఎక్స్‌ప్రెషన్ కూడా కర్లీ బ్రేసెస్ మధ్య పనిచేస్తుంది, ఉదాహరణకు `formatDate()` ఫంక్షన్ కాల్:

<Sandpack>

```js
const today = new Date();

function formatDate(date) {
  return new Intl.DateTimeFormat(
    'en-US',
    { weekday: 'long' }
  ).format(date);
}

export default function TodoList() {
  return (
    <h1>To Do List for {formatDate(today)}</h1>
  );
}
```

</Sandpack>

### కర్లీ బ్రేసెస్ ఎక్కడ ఉపయోగించాలి {/*where-to-use-curly-braces*/}

మీరు JSX లో కర్లీ బ్రేసెస్ ను రెండు విధాలుగా మాత్రమే ఉపయోగించవచ్చు:

1. **టెక్స్ట్ గా** JSX ట్యాగ్ లో నేరుగా: `<h1>{name}'s To Do List</h1>` పనిచేస్తుంది, కానీ `<{tag}>Gregorio Y. Zara's To Do List</{tag}>`  పనిచేయదు.
2. **అట్రిబ్యూట్స్ గా** `=` సైన్ వెంటనే: `src={avatar}` అనేది `avatar` వేరియబుల్ ను చదువుతుంది, కానీ `src="{avatar}"` అనేది `"{avatar}"` string ను పాస్ చేస్తుంది.

## "డబుల్ కర్లీస్" ఉపయోగించడం: JSX లో CSS మరియు ఇతర ఆబ్జెక్టులు {/*using-double-curlies-css-and-other-objects-in-jsx*/}

strings, నంబర్స్ మరియు ఇతర JavaScript ఎక్స్‌ప్రెషన్స్‌ ను మించి, మీరు JSX లో ఆబ్జెక్ట్‌లను కూడా పాస్ చేయవచ్చు. ఆబ్జెక్ట్స్‌ను కూడా కర్లీ బ్రేసెస్‌తో చూపిస్తారు, ఉదాహరణకు `{ name: "Hedy Lamarr", inventions: 5 }`. అందువల్ల, JavaScript ఆబ్జెక్ట్‌ను JSX లో పాస్ చేయడానికి మీరు దానిని మరో కర్లీ బ్రేసెస్ జంటలో ఉంచాలి: `person={{ name: "Hedy Lamarr", inventions: 5 }}`.

మీరు దీన్ని JSX లో ఇన్‌లైన్ CSS స్టైల్‌లతో చూడవచ్చు. React ఇన్‌లైన్ స్టైల్‌లను ఉపయోగించమని నిర్దిష్టంగా చెప్పదు (CSS class లు చాలా సందర్భాలలో బాగానే పనిచేస్తాయి). కానీ మీరు ఇన్‌లైన్ స్టైల్ అవసరం ఉన్నప్పుడు, మీరు ఆ `style` అట్రిబ్యూట్‌కు ఒక ఆబ్జెక్ట్ పంపాలి:

<Sandpack>

```js
export default function TodoList() {
  return (
    <ul style={{
      backgroundColor: 'black',
      color: 'pink'
    }}>
      <li>Improve the videophone</li>
      <li>Prepare aeronautics lectures</li>
      <li>Work on the alcohol-fuelled engine</li>
    </ul>
  );
}
```

```css
body { padding: 0; margin: 0 }
ul { padding: 20px 20px 20px 40px; margin: 0; }
```

</Sandpack>

`backgroundColor` మరియు `color` వాల్యూలను మార్చే ప్రయత్నం చేయండి.

మీరు కర్లీ బ్రేసెస్ లో JavaScript ఆబ్జెక్టును ఇలా రాసినప్పుడు, మీరు ఆ ఆబ్జెక్టును నిజంగా చూడవచ్చు:

```js {2-5}
<ul style={
  {
    backgroundColor: 'black',
    color: 'pink'
  }
}>
```

తదుపరి మీరు JSX లో `{{` మరియు `}}` చూసినప్పుడు, అవి JSX కర్లీ బ్రేసెస్‌లో ఉన్న ఒక ఆబ్జెక్ట్ మాత్రమే అని గుర్తించండి!

<Pitfall>

ఇన్‌లైన్ `style` ప్రాపర్టీలు camelCase లో రాయాలి. ఉదాహరణకు, HTML `<ul style="background-color: black">` JSX లో `<ul style={{ backgroundColor: 'black' }}>` అనే విధంగా రాయబడుతుంది.

</Pitfall>

## మరింత సరదా JavaScript ఆబ్జెక్టులతో మరియు కర్లీ బ్రేసెస్‌తో {/*more-fun-with-javascript-objects-and-curly-braces*/}

మీరు చాలా ఎక్స్‌ప్రెషన్లను ఒక ఆబ్జెక్ట్‌లోకి తీసుకెళ్లి, వాటిని మీ JSX లో కర్లీ బ్రేసెస్ లో రిఫరెన్స్ చేయవచ్చు:

<Sandpack>

```js
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src="https://i.imgur.com/7vQD0fPs.jpg"
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

```css
body { padding: 0; margin: 0 }
body > div > div { padding: 20px; }
.avatar { border-radius: 50%; height: 90px; }
```

</Sandpack>

ఈ ఉదాహరణలో, `person` JavaScript ఆబ్జెక్ట్‌లో ఒక `name` string మరియు ఒక `theme` ఆబ్జెక్ట్ ఉన్నాయి:

```js
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};
```

కంపోనెంట్ ఈ వాల్యూను `person` నుండి ఇలా ఉపయోగించవచ్చు:

```js
<div style={person.theme}>
  <h1>{person.name}'s Todos</h1>
```

JSX ఒక టెంప్లేటింగ్ లాంగ్వేజ్‌గా చాలా సాధారణంగా ఉంటుంది ఎందుకంటే ఇది JavaScript ఉపయోగించి డేటా మరియు లాజిక్‌ను నిర్వహించడానికి సహాయపడుతుంది.

<Recap>

ఇప్పుడు మీరు JSX గురించి చాలా విషయాలను తెలుసుకున్నారు:

* JSX అట్రిబ్యూట్‌లు కోట్స్‌లో strings గా పంపబడతాయి.
* కర్లీ బ్రేసెస్ JavaScript లాజిక్ మరియు వేరియబుల్స్‌ను మీ మార్కప్‌లో చేర్చడానికి అనుమతిస్తాయి.
* అవి JSX ట్యాగ్ కంటెంట్ లో లేదా అట్రిబ్యూట్స్‌లో `=` తర్వాత పనిచేస్తాయి.
* `{{` మరియు `}}` ప్రత్యేక సింటాక్స్ కాదు: ఇవి JSX కర్లీ బ్రేసెస్‌లో వేసిన JavaScript ఆబ్జెక్ట్.

</Recap>

<Challenges>

#### తప్పును సరిచేయండి {/*fix-the-mistake*/}

ఈ కోడ్ `Objects are not valid as a React child` అనే ఎర్రర్ తో క్రాష్ అవుతోంది:

<Sandpack>

```js
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person}'s Todos</h1>
      <img
        className="avatar"
        src="https://i.imgur.com/7vQD0fPs.jpg"
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

```css
body { padding: 0; margin: 0 }
body > div > div { padding: 20px; }
.avatar { border-radius: 50%; height: 90px; }
```

</Sandpack>

మీరు సమస్యను కనుగొనగలరా?

<Hint>కర్లీ బ్రేసెస్‌లో ఏమి ఉంది అనే దానిని చూడండి. మనం అక్కడ సరైన వాటిని ఉంచుతున్నామా?</Hint>

<Solution>

ఇది ఇలా జరుగుతోంది ఎందుకంటే ఈ ఉదాహరణలో **ఒక ఆబ్జెక్ట్‌ను స్వయంగా** స్ట్రింగ్ స్థానంలో మార్కప్‌లో రెండర్ చేయడానికి ప్రయత్నిస్తోంది: `<h1>{person}'s Todos</h1>` మొత్తం `person` ఆబ్జెక్ట్‌ను రెండర్ చేయడానికి ప్రయత్నిస్తోంది! Raw ఆబ్జెక్ట్స్‌ను టెక్స్ట్ కంటెంట్‌గా చేర్చడం వల్ల ఒక ఎర్రర్ వస్తుంది, ఎందుకంటే React వాటిని మీరు ఎలా చూపించాలనుకుంటున్నారో అర్థం చేసుకోలేకపోతుంది.

దీన్ని సరి చేయడానికి, `<h1>{person}'s Todos</h1>` ను `<h1>{person.name}'s Todos</h1>` తో మార్చండి:

<Sandpack>

```js
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src="https://i.imgur.com/7vQD0fPs.jpg"
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

```css
body { padding: 0; margin: 0 }
body > div > div { padding: 20px; }
.avatar { border-radius: 50%; height: 90px; }
```

</Sandpack>

</Solution>

#### సమాచారాన్ని ఒక ఆబ్జెక్టులోకి తీసుకోండి {/*extract-information-into-an-object*/}

చిత్రం URL ని `person` ఆబ్జెక్టులోకి తీసుకోండి.

<Sandpack>

```js
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src="https://i.imgur.com/7vQD0fPs.jpg"
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

```css
body { padding: 0; margin: 0 }
body > div > div { padding: 20px; }
.avatar { border-radius: 50%; height: 90px; }
```

</Sandpack>

<Solution>

చిత్రం URL ను `person.imageUrl` అనే ప్రాపర్టీగా మార్చండి మరియు `<img>` ట్యాగ్ నుండి దీన్ని కర్లీ బ్రేసెస్ ఉపయోగించి చదవండి:

<Sandpack>

```js
const person = {
  name: 'Gregorio Y. Zara',
  imageUrl: "https://i.imgur.com/7vQD0fPs.jpg",
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src={person.imageUrl}
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

```css
body { padding: 0; margin: 0 }
body > div > div { padding: 20px; }
.avatar { border-radius: 50%; height: 90px; }
```

</Sandpack>

</Solution>

#### JSX కర్లీ బ్రేసెస్‌లో ఒక ఎక్స్‌ప్రెషన్ రాయండి {/*write-an-expression-inside-jsx-curly-braces*/}

కింద ఇచ్చిన ఆబ్జెక్టులో, పూర్తి చిత్రం URL నాలుగు భాగాల్లో విభజించబడింది: బేస్ URL, `imageId`, `imageSize`, మరియు ఫైల్ ఎక్స్‌టెన్షన్.

మేము ఈ అట్రిబ్యూట్లను కలిపి చిత్రం URL తయారుచేయాలని కోరుకుంటున్నాము: బేస్ URL (ఎప్పుడూ `'https://i.imgur.com/'`), `imageId` (`'7vQD0fP'`), `imageSize` (`'s'`), మరియు ఫైల్ ఎక్స్‌టెన్షన్ (ఎప్పుడూ `'.jpg'`). అయితే, `<img>` ట్యాగ్ లో `src` ఎలా నిర్దేశించబడింది అనేదిలో ఏదో తప్పు ఉంది.

మీరు దీనిని సరి చేయగలరా?

<Sandpack>

```js

const baseUrl = 'https://i.imgur.com/';
const person = {
  name: 'Gregorio Y. Zara',
  imageId: '7vQD0fP',
  imageSize: 's',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src="{baseUrl}{person.imageId}{person.imageSize}.jpg"
        alt={person.name}
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

```css
body { padding: 0; margin: 0 }
body > div > div { padding: 20px; }
.avatar { border-radius: 50%; }
```

</Sandpack>

మీ ఫిక్స్ పనిచేసిందో చూడడానికి, `imageSize` వాల్యూ `'b'` గా మార్చండి. మీ మార్పు తర్వాత చిత్రం పరిమాణం మారుతుంది.

<Solution>

మీరు దీనిని ఇలా రాయవచ్చు: `src={baseUrl + person.imageId + person.imageSize + '.jpg'}`.

1. `{` JavaScript ఎక్స్‌ప్రెషన్‌ను ప్రారంభిస్తుంది
2. `baseUrl + person.imageId + person.imageSize + '.jpg'` సరైన URL string ను ఉత్పత్తి చేస్తుంది
3. `}` JavaScript ఎక్స్‌ప్రెషన్‌ను ముగిస్తుంది

<Sandpack>

```js
const baseUrl = 'https://i.imgur.com/';
const person = {
  name: 'Gregorio Y. Zara',
  imageId: '7vQD0fP',
  imageSize: 's',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src={baseUrl + person.imageId + person.imageSize + '.jpg'}
        alt={person.name}
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

```css
body { padding: 0; margin: 0 }
body > div > div { padding: 20px; }
.avatar { border-radius: 50%; }
```

</Sandpack>

మీరు ఈ ఎక్స్‌ప్రెషన్‌ను ప్రత్యేకమైన ఫంక్షన్‌గా కూడా మార్చవచ్చు, ఉదాహరణకు `getImageUrl`:

<Sandpack>

```js src/App.js
import { getImageUrl } from './utils.js'

const person = {
  name: 'Gregorio Y. Zara',
  imageId: '7vQD0fP',
  imageSize: 's',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src={getImageUrl(person)}
        alt={person.name}
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

```js src/utils.js
export function getImageUrl(person) {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    person.imageSize +
    '.jpg'
  );
}
```

```css
body { padding: 0; margin: 0 }
body > div > div { padding: 20px; }
.avatar { border-radius: 50%; }
```

</Sandpack>

మార్కప్‌ను సింపుల్ గా ఉంచడానికి వేరియబుల్స్ మరియు ఫంక్షన్లు సహాయపడతాయి!

</Solution>

</Challenges>
