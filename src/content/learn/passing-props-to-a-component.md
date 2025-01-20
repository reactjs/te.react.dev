---
title: కంపోనెంట్‌కు Props పాస్ చేయడం
---

<Intro>

React కంపోనెంట్‌లు *props* ను ఒకదానితో ఒకటి కమ్యూనికేట్ చేసుకునేందుకు ఉపయోగిస్తాయి. ప్రతి పేరెంట్ కంపోనెంట్ దాని చైల్డ్ కంపోనెంట్‌లకు props ద్వారా కొంత సమాచారం పాస్ చేయవచ్చు. Props మీకు HTML ఆట్రిబ్యుట్‌లను గుర్తు చేయవచ్చు, కానీ మీరు వాటి ద్వారా ఆబ్జెక్ట్‌లు, అర్రేలు, ఫంక్షన్‌లు వంటి ఏదైనా జావాస్క్రిప్ట్ విలువలను పాస్ చేయవచ్చు.

</Intro>

<YouWillLearn>

* ఎలా props ను ఒక కంపోనెంట్‌కు పాస్ చేయాలి
* ఎలా props ను ఒక కంపోనెంట్‌లో చదవాలి
* props కోసం డిఫాల్ట్ విలువలు ఎలా స్పెసిఫై చేయాలి props
* కొంత JSX ను కంపోనెంట్‌కు ఎలా పాస్ చేయాలి
* ఎలా props కాలక్రమంలో మారతాయి

</YouWillLearn>

## తెలిసిన props {/*familiar-props*/}

Props అనేవి మీరు JSX ట్యాగ్‌కు పాస్ చేసే సమాచారం. ఉదాహరణకు, `className`, `src`, `alt`, `width`, మరియు `height` ఇవి మీరు `<img>` ట్యాగ్‌కు పాస్ చేయగల props:

<Sandpack>

```js
function Avatar() {
  return (
    <img
      className="avatar"
      src="https://i.imgur.com/1bX5QH6.jpg"
      alt="Lin Lanying"
      width={100}
      height={100}
    />
  );
}

export default function Profile() {
  return (
    <Avatar />
  );
}
```

```css
body { min-height: 120px; }
.avatar { margin: 20px; border-radius: 50%; }
```

</Sandpack>

మీరు `<img>` ట్యాగ్‌కు పాస్ చేయగల props ముందే నిర్ణయించినవి (ReactDOM దీనికి అనుగుణంగా ఉంటుంది [HTML ప్రమాణం](https://www.w3.org/TR/html52/semantics-embedded-content.html#the-img-element)). మీరు ఏవైనా ప్రాప్‌లను *మీ స్వంత* భాగాలకు పాస్ చేయవచ్చు, ఉదాహరణకు `<Avatar>`, వాటిని అనుకూలీకరించడానికి (to customize them). ఇలా చేయండి!

## కంపోనెంట్‌కు props పాస్ చేయడం {/*passing-props-to-a-component*/}

ఈ కోడ్‌లో, `Profile` కంపోనెంట్ తన చైల్డ్ కంపోనెంట్ అయిన `Avatar` కు ఎలాంటి props ని పాస్ చేయడంలేదు:

```js
export default function Profile() {
  return (
    <Avatar />
  );
}
```

మీరు `Avatar` కు రెండు రకాలుక props ఇవ్వవచ్చు.

### స్టెప్ 1: చైల్డ్ కంపోనెంట్‌కు props పాస్ చేయండి. {/*step-1-pass-props-to-the-child-component*/}

మొదట, `Avatar` కు కొన్ని props పాస్ చేయండి. ఉదాహరణకు, రెండు props పాస్ చేద్దాం: `person` (an object) మరియు `size` (a number):

```js
export default function Profile() {
  return (
    <Avatar
      person={{ name: 'Lin Lanying', imageId: '1bX5QH6' }}
      size={100}
    />
  );
}
```

<Note>

`person=` తరువాత డబుల్ కర్లీ బ్రాకెట్స్ మీకు సందేహం కలిగిస్తే, అవి JSX కర్లీస్ [ఒక ఆబ్జెక్ట్ మాత్రమే](/learn/javascript-in-jsx-with-curly-braces#using-double-curlies-css-and-other-objects-in-jsx) అని గుర్తుంచుకోండి.

</Note>

ఇప్పుడు మీరు ఈ props ను `Avatar` కంపోనెంట్ లో చదవచ్చు.

### స్టెప్ 2: చైల్డ్ కంపోనెంట్ లో props ను చదవండి. {/*step-2-read-props-inside-the-child-component*/}

మీరు ఈ props ను `function Avatar` తర్వాత నేరుగా `({` మరియు `})` లో కమాలతో వేరు చేసిన `person, size` పేర్లను జాబితా చేయడం ద్వారా చదవచ్చు. ఇది మీకు `Avatar` కోడ్ లో వేరియబుల్ వంటి వాటిని ఉపయోగించడానికి అనుమతిస్తుంది.

```js
function Avatar({ person, size }) {
  // person and size are available here
}
```

`Avatar` లో `person` మరియు `size` props ను ఉపయోగించి రెండరింగ్ కోసం కొంత లాజిక్ జోడించండి, అంతే మీ పని పూర్తవుతుంది.

ఇప్పుడు మీరు `Avatar` ను వివిధ props తో అనేక రకాలుగా రెండర్ చేయడానికి కాన్ఫిగర్ చేయవచ్చు. వాల్యూ మార్చి ప్రయత్నించండి!

<Sandpack>

```js src/App.js
import { getImageUrl } from './utils.js';

function Avatar({ person, size }) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

export default function Profile() {
  return (
    <div>
      <Avatar
        size={100}
        person={{ 
          name: 'Katsuko Saruhashi', 
          imageId: 'YfeOqp2'
        }}
      />
      <Avatar
        size={80}
        person={{
          name: 'Aklilu Lemma', 
          imageId: 'OKS67lh'
        }}
      />
      <Avatar
        size={50}
        person={{ 
          name: 'Lin Lanying',
          imageId: '1bX5QH6'
        }}
      />
    </div>
  );
}
```

```js src/utils.js
export function getImageUrl(person, size = 's') {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    size +
    '.jpg'
  );
}
```

```css
body { min-height: 120px; }
.avatar { margin: 10px; border-radius: 50%; }
```

</Sandpack>

Props మీకు పేరెంట్ మరియు చైల్డ్ కంపోనెంట్‌లను స్వతంత్రంగా ఆలోచించడానికి అనుమతిస్తాయి. ఉదాహరణకు, మీరు `Profile` లో `person` లేదా `size` props ను మార్చవచ్చు, కానీ `Avatar` అవి ఎలా ఉపయోగిస్తుందో గురించి ఆలోచించాల్సిన అవసరం లేదు. అదేవిధంగా, మీరు `Avatar` ఈ props ను ఎలా ఉపయోగిస్తుందో మార్చవచ్చు, `Profile` ను చూడకుండా.

మీరు props ను "knobs" లాగా అనుకోవచ్చు, వాటిని మీరు సర్దుబాటు చేయవచ్చు. ఇవి ఫంక్షన్‌లకు ఆర్గుమెంట్‌లు ఎంత ముఖ్యమో, అదే పాత్ర పోషిస్తాయి—వాస్తవానికి, props మీ కంపోనెంట్‌కు కలిగే ఏకైక ఆర్గుమెంట్! React కంపోనెంట్ ఫంక్షన్‌లు ఒకే ఆర్గుమెంట్, అంటే `props` ఆబ్జెక్ట్‌ను స్వీకరిస్తాయి:

```js
function Avatar(props) {
  let person = props.person;
  let size = props.size;
  // ...
}
```

సాధారణంగా, మీకు మొత్తం `props` ఆబ్జెక్ట్ అవసరం ఉండదు, కాబట్టి మీరు దానిని విడగొట్టి సొంతంగా props గా ఉపయోగిస్తారు.

<Pitfall>

**props డిక్లేర్ చేస్తూ `{` మరియు `}` కర్లీస్ జత** `(` మరియు `)` లోపల మిస్ చేయకండి.

```js
function Avatar({ person, size }) {
  // ...
}
```

ఈ సింటాక్స్‌ను ["డీస్ట్రక్చరింగ్"](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Unpacking_fields_from_objects_passed_as_a_function_parameter) అని పిలుస్తారు ఇది ఒక ఫంక్షన్ పరమేటర్ నుండి ప్రాపర్టీలు చదవడానికి సమానమైనది:

```js
function Avatar(props) {
  let person = props.person;
  let size = props.size;
  // ...
}
```

</Pitfall>

## prop డిఫాల్ట్ వాల్యూ స్పెసిఫై చేయడం {/*specifying-a-default-value-for-a-prop*/}

మీరు prop కి డిఫాల్ట్ వాల్యూ ఇచ్చి, ఎలాంటి వాల్యూ నిర్దేశించకుండా వదిలేస్తే అది డిఫాల్ట్ వాల్యూ పడ్డప్పుడు, మీరు డీస్ట్రక్చరింగ్ ద్వారా `=` డిఫాల్ట్ వాల్యూ పరమేటర్ తర్వాత పెట్టి ఇది చేయవచ్చు:

```js
function Avatar({ person, size = 100 }) {
  // ...
}
```

ఇప్పుడు, ఏదైనా `size` prop లేకుండా `<Avatar person={...} />` రెండర్ అయితే, `size` వాల్యూ `100` గా సెట్ అవుతుంది.

డిఫాల్ట్ వాల్యూ మాత్రమే `size` prop మిస్సయితే లేదా `size={undefined}` పాస్ చేసినప్పుడు ఉపయోగించబడుతుంది. కానీ మీరు `size={null}` లేదా `size={0}` పాస్ చేస్తే, డిఫాల్ట్ వాల్యూ **ఉపయోగించబడదు**.

## JSX స్ప్రెడ్ సింటాక్స్ ద్వారా props ఫార్వర్డ్ చేయడం {/*forwarding-props-with-the-jsx-spread-syntax*/}

కొన్నిసార్లు, props ఇవ్వడం చాలా బోర్ కొడుతుంది:

```js
function Profile({ person, size, isSepia, thickBorder }) {
  return (
    <div className="card">
      <Avatar
        person={person}
        size={size}
        isSepia={isSepia}
        thickBorder={thickBorder}
      />
    </div>
  );
}
```

తరుచుగా వాడే కోడ్‌లో ఎలాంటి తప్పు లేదు—అది మరింత స్పష్టంగా చదవగలిగేది కావచ్చు. కానీ కొన్నిసార్లు మీరు సంక్షిప్తతకు విలువ ఇస్తారు. కొన్ని కంపోనెంట్‌లు తమ props ను అన్ని చైల్డ్‌లకు ఫార్వర్డ్ చేస్తాయి, ఉదాహరణకు, ఈ `Profile` లో `Avatar` props పాస్ చేసిన విధానం. అవి తమ props ను నేరుగా ఉపయోగించకపోతే, మరింత కొద్దిపాటి "స్ప్రెడ్" సింటాక్స్ ఉపయోగించడం సరైనది కావచ్చు:

```js
function Profile(props) {
  return (
    <div className="card">
      <Avatar {...props} />
    </div>
  );
}
```

ఇది `Profile` లోని అన్ని props లను వాటి పేర్లను లేకుండా `Avatar` కు ఫార్వర్డ్ చేస్తుంది.

**స్ప్రెడ్ సింటాక్స్‌ను లిమిటెడ్ కా ఉపయోగించండి.** మీరు దాన్ని ప్రతి ఇతర కంపోనెంట్‌లో ఉపయోగిస్తే, దాంట్లో ఏదో పొరపాటు ఉంది. ఇది తరచుగా మీ కంపోనెంట్‌లను విడిగ, చిల్డ్రన్‌ను JSX‌ గా పాస్ చేయాలని చూస్తుంది. దీని గురించి మరింత తరువాత తెలుసుకుందాం!

## JSX ని చిల్డ్రన్‌గా పాస్ చేయడం {/*passing-jsx-as-children*/}

బిల్ట్-ఇన్ బ్రౌజర్ ట్యాగ్‌లను నెస్టింగ్ చేయడం సాధారణ ప్రాక్టీస్:

```js
<div>
  <img />
</div>
```

కొన్నిసార్లు మీరు మీ సొంత కంపోనెంట్‌లను కూడా అదే విధంగా నెస్ట్ చేయాలని కోరుకుంటారు:

```js
<Card>
  <Avatar />
</Card>
```

మీరు JSX ట్యాగ్‌లో కంటెంట్‌ను నెస్ట్ చేస్తే, పేర్ెంట్ కంపోనెంట్ ఆ కంటెంట్‌ను `children` అనే prop లో స్వీకరిస్తుంది. ఉదాహరణకు, కింద ఇచ్చిన `Card` కంపోనెంట్ `<Avatar />` ను `children` prop గా స్వీకరిస్తుంది మరియు దాన్ని ఒక రేపర్‌ల `div` లో రెండర్ చేస్తుంది:

<Sandpack>

```js src/App.js
import Avatar from './Avatar.js';

function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

export default function Profile() {
  return (
    <Card>
      <Avatar
        size={100}
        person={{ 
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />
    </Card>
  );
}
```

```js src/Avatar.js
import { getImageUrl } from './utils.js';

export default function Avatar({ person, size }) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}
```

```js src/utils.js
export function getImageUrl(person, size = 's') {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    size +
    '.jpg'
  );
}
```

```css
.card {
  width: fit-content;
  margin: 5px;
  padding: 5px;
  font-size: 20px;
  text-align: center;
  border: 1px solid #aaa;
  border-radius: 20px;
  background: #fff;
}
.avatar {
  margin: 20px;
  border-radius: 50%;
}
```

</Sandpack>

`<Card>` లోని `<Avatar>` ను కొన్ని టెక్స్ట్‌తో మార్చి ప్రయత్నించండి, అప్పుడు `Card` కంపోనెంట్ ఎలాంటి నెస్టెడ్ కంటెంట్‌ను అయినా ఎలా ర్యాప్ చేయగలదో మీరు గమనించవచ్చు. దాని లోపల ఏమి రెండర్ అవుతుందో "తెలుసుకోవాల్సిన" అవసరం దీనికి లేదు. మీరు చాలా చోట్ల ఈ సౌకర్యవంతమైన పాటర్న్ చూస్తారు.

`children` prop ఉన్న ఒక కాంపోనెంట్‌ను దాని పేరెంట్ కాంపోనెంట్‌ల ద్వారా ఆర్బిట్రరీ JSX తో "నింపగల" "రంధ్రం" కలిగి ఉన్నట్లు మీరు అనుకోవచ్చు. మీరు తరచుగా విజువల్ రేపర్‌ల కోసం `children` prop ఉపయోగిస్తారు: ప్యానెల్‌లు, గ్రిడ్‌లు మొదలైనవి.

<Illustration src="/images/docs/illustrations/i_children-prop.png" alt='A puzzle-like Card tile with a slot for "children" pieces like text and Avatar' />

## Props కాలక్రమేణా ఎలా మారుతాయో {/*how-props-change-over-time*/}

కింద ఇచ్చిన `Clock` కంపోనెంట్ దాని పేర్ెంట్ కంపోనెంట్ నుండి రెండు ప్రాప్స్‌ని స్వీకరిస్తుంది: `color` మరియు `time`. (పేర్ెంట్ కంపోనెంట్ కోడ్‌ను మినహాయించారు, ఎందుకంటే అది [state](/learn/state-a-components-memory) ను ఉపయోగిస్తుంది, దానిపై మనం ఇప్పుడే చర్చించటం లేదు.)

కింద ఉన్న సెలెక్ట్ బాక్స్‌లో రంగును మార్చి చూడండి:

<Sandpack>

```js src/Clock.js active
export default function Clock({ color, time }) {
  return (
    <h1 style={{ color: color }}>
      {time}
    </h1>
  );
}
```

```js src/App.js hidden
import { useState, useEffect } from 'react';
import Clock from './Clock.js';

function useTime() {
  const [time, setTime] = useState(() => new Date());
  useEffect(() => {
    const id = setInterval(() => {
      setTime(new Date());
    }, 1000);
    return () => clearInterval(id);
  }, []);
  return time;
}

export default function App() {
  const time = useTime();
  const [color, setColor] = useState('lightcoral');
  return (
    <div>
      <p>
        Pick a color:{' '}
        <select value={color} onChange={e => setColor(e.target.value)}>
          <option value="lightcoral">lightcoral</option>
          <option value="midnightblue">midnightblue</option>
          <option value="rebeccapurple">rebeccapurple</option>
        </select>
      </p>
      <Clock color={color} time={time.toLocaleTimeString()} />
    </div>
  );
}
```

</Sandpack>

ఈ ఉదాహరణ **ఒక కంపోనెంట్ సమయం గడిచేకొద్దీ వేర్వేరు props పొందవచ్చు** అని చూపిస్తుంది. Props ఎప్పుడూ స్థిరంగా ఉండవు! ఇక్కడ, `time` prop ప్రతి సెకనుకు మారుతుంది, మరియు `color` ప్రాప్ మీరు మరో రంగును ఎంచుకున్నప్పుడు మారుతుంది. Props ఒక కంపోనెంట్ యొక్క డేటాను ఎప్పుడైనా ప్రతిబింబిస్తాయి, మొదట్లో మాత్రమే కాదు.

అయితే, props [ఇమ్మ్యుటబుల్](https://en.wikipedia.org/wiki/Immutable_object)—ఇది కంప్యూటర్ సైన్స్ లో "మార్చలేనిది" అనే అర్థం కలిగిన పదం. ఒక కంపోనెంట్ దాని props మార్చాల్సినప్పుడు (ఉదాహరణకు, యూజర్ చర్య లేదా కొత్త డేటాకు ప్రతిస్పందనగా), అది దాని పేరెంట్ కంపోనెంట్ props _వేరే props_-కొత్త ఆబ్జెక్ట్‌ను పంపించమని "ఆరాధించాలి"! దాని పాత props తరువాత దూరంగా వేయబడతాయి, మరియు చివరికి జావాస్క్రిప్ట్ ఇంజిన్ వాటి ద్వారా తీసుకున్న మెమరీని తిరిగి స్వీకరిస్తుంది.

**"Props మార్చడానికి ప్రయత్నించకండి".** మీరు యూజర్ ఇన్పుట్ (ఎంచుకున్న రంగును మార్చడం వంటి) కి స్పందించాల్సినప్పుడు, మీరు "state సెట్ చేయాలి", దానిపై మీరు [State: A Component's Memory.](/learn/state-a-components-memory) లో తెలుసుకోవచ్చు

<Recap>

* Props పంపించడానికి, వాటిని JSX లో జోడించండి, మీరు HTML అట్రిబ్యూషన్లతో చేసినట్లే.
* Props ను చదవడానికి, `function Avatar({ person, size })` డెస్ట్రక్చరింగ్ సింటాక్స్ ఉపయోగించండి.
* మీరు `size = 100` వంటి డిఫాల్ట్ వాల్యూ స్పెసిఫై చేయవచ్చు, ఇది లేకపోతే మరియు `undefined` props కోసం ఉపయోగించబడుతుంది.
* మీరు `<Avatar {...props} />` JSX స్ప్రెడ్ సింటాక్స్‌తో అన్ని props ఫార్వర్డ్ చేయవచ్చు, కానీ దీనిని ఎక్కువగా ఉపయోగించకండి!
* `<Card><Avatar /></Card>` వంటి నెస్టెడ్ JSX `Card` కంపోనెంట్ యొక్క `children` prop కనిపిస్తుంది.
*  Props సమయానికి చదవడానికి మాత్రమే స్నాప్‌షార్ట్: ప్రతి రెండరింగ్ ఒక కొత్త props వెర్షన్‌ను అందిస్తుంది.
* మీరు props మార్చలేరు. మీరు ఇంటరాక్టివిటీ అవసరమైనప్పుడు, state సెట్ చేయాల్సి ఉంటుంది.

</Recap>



<Challenges>

#### కంపోనెంట్‌ను ఎక్స్‌ట్రాక్ట్ చేయండి {/*extract-a-component*/}

ఈ `Gallery` కంపోనెంట్‌లో రెండు ప్రొఫైళ్లకు సంబంధించిన చాలా సమానమైన మార్కప్ ఉంది. డుప్లికేషన్‌ను తగ్గించేందుకు దీని నుండి ఒక `Profile` కంపోనెంట్‌ను ఎక్స్‌ట్రాక్ట్ చేయండి. దీనికి ఏమి props పంపాలనేది మీరు నిర్ణయించుకోవాలి.

<Sandpack>

```js src/App.js
import { getImageUrl } from './utils.js';

export default function Gallery() {
  return (
    <div>
      <h1>Notable Scientists</h1>
      <section className="profile">
        <h2>Maria Skłodowska-Curie</h2>
        <img
          className="avatar"
          src={getImageUrl('szV5sdG')}
          alt="Maria Skłodowska-Curie"
          width={70}
          height={70}
        />
        <ul>
          <li>
            <b>Profession: </b> 
            physicist and chemist
          </li>
          <li>
            <b>Awards: 4 </b> 
            (Nobel Prize in Physics, Nobel Prize in Chemistry, Davy Medal, Matteucci Medal)
          </li>
          <li>
            <b>Discovered: </b>
            polonium (chemical element)
          </li>
        </ul>
      </section>
      <section className="profile">
        <h2>Katsuko Saruhashi</h2>
        <img
          className="avatar"
          src={getImageUrl('YfeOqp2')}
          alt="Katsuko Saruhashi"
          width={70}
          height={70}
        />
        <ul>
          <li>
            <b>Profession: </b> 
            geochemist
          </li>
          <li>
            <b>Awards: 2 </b> 
            (Miyake Prize for geochemistry, Tanaka Prize)
          </li>
          <li>
            <b>Discovered: </b>
            a method for measuring carbon dioxide in seawater
          </li>
        </ul>
      </section>
    </div>
  );
}
```

```js src/utils.js
export function getImageUrl(imageId, size = 's') {
  return (
    'https://i.imgur.com/' +
    imageId +
    size +
    '.jpg'
  );
}
```

```css
.avatar { margin: 5px; border-radius: 50%; min-height: 70px; }
.profile {
  border: 1px solid #aaa;
  border-radius: 6px;
  margin-top: 20px;
  padding: 10px;
}
h1, h2 { margin: 5px; }
h1 { margin-bottom: 10px; }
ul { padding: 0px 10px 0px 20px; }
li { margin: 5px; }
```

</Sandpack>

<Hint>

మొదట ఒక శాస్త్రవేత్తకు సంబంధించిన మార్కప్‌ను ఎక్స్‌ట్రాక్ట్ చేయడం ప్రారంభించండి. ఆపై, రెండో ఉదాహరణలో వాటితో సరిపోని భాగాలను గుర్తించండి మరియు వాటిని props ద్వారా కాన్ఫిగర్ చేయగలిగేలా చేయండి.

</Hint>

<Solution>

ఈ పరిష్కారంలో, `Profile` కంపోనెంట్ అనేక props లను అందుకుంటుంది: `imageId` (a string), `name` (a string), `profession` (a string), `awards` (an array of strings), `discovery` (a string), `imageSize` (a number).

గమనించండి, `imageSize` prop కు ఒక డిఫాల్ట్ వాల్యూ ఉంది, అందువల్ల దాన్ని కంపోనెంట్‌కు పంపించవలసిన అవసరం లేదు.

<Sandpack>

```js src/App.js
import { getImageUrl } from './utils.js';

function Profile({
  imageId,
  name,
  profession,
  awards,
  discovery,
  imageSize = 70
}) {
  return (
    <section className="profile">
      <h2>{name}</h2>
      <img
        className="avatar"
        src={getImageUrl(imageId)}
        alt={name}
        width={imageSize}
        height={imageSize}
      />
      <ul>
        <li><b>Profession:</b> {profession}</li>
        <li>
          <b>Awards: {awards.length} </b>
          ({awards.join(', ')})
        </li>
        <li>
          <b>Discovered: </b>
          {discovery}
        </li>
      </ul>
    </section>
  );
}

export default function Gallery() {
  return (
    <div>
      <h1>Notable Scientists</h1>
      <Profile
        imageId="szV5sdG"
        name="Maria Skłodowska-Curie"
        profession="physicist and chemist"
        discovery="polonium (chemical element)"
        awards={[
          'Nobel Prize in Physics',
          'Nobel Prize in Chemistry',
          'Davy Medal',
          'Matteucci Medal'
        ]}
      />
      <Profile
        imageId='YfeOqp2'
        name='Katsuko Saruhashi'
        profession='geochemist'
        discovery="a method for measuring carbon dioxide in seawater"
        awards={[
          'Miyake Prize for geochemistry',
          'Tanaka Prize'
        ]}
      />
    </div>
  );
}
```

```js src/utils.js
export function getImageUrl(imageId, size = 's') {
  return (
    'https://i.imgur.com/' +
    imageId +
    size +
    '.jpg'
  );
}
```

```css
.avatar { margin: 5px; border-radius: 50%; min-height: 70px; }
.profile {
  border: 1px solid #aaa;
  border-radius: 6px;
  margin-top: 20px;
  padding: 10px;
}
h1, h2 { margin: 5px; }
h1 { margin-bottom: 10px; }
ul { padding: 0px 10px 0px 20px; }
li { margin: 5px; }
```

</Sandpack>

గమనించండి, `awards` ఒక array అయితే, మీరు ప్రత్యేకంగా `awardCount` prop అవసరం లేకుండా `awards.length`ను ఉపయోగించి అవార్డుల సంఖ్యను లెక్కించవచ్చు. గుర్తుంచుకోండి, props ఏవైనా వాల్యుస్ తీసుకోగలవు, వీటిలో arrays కూడా ఉన్నాయి!

మరొక పరిష్కారం, ఈ పేజీలోని గత ఉదాహరణలతో మరింత సమానం, అంటే వ్యక్తి గురించి అన్ని సమాచారం ఒకే ఆబ్జెక్ట్‌లో గ్రూప్ చేయడం మరియు ఆ ఆబ్జెక్ట్‌ను ఒకే prop గా పాస్ చేయడం:

<Sandpack>

```js src/App.js
import { getImageUrl } from './utils.js';

function Profile({ person, imageSize = 70 }) {
  const imageSrc = getImageUrl(person)

  return (
    <section className="profile">
      <h2>{person.name}</h2>
      <img
        className="avatar"
        src={imageSrc}
        alt={person.name}
        width={imageSize}
        height={imageSize}
      />
      <ul>
        <li>
          <b>Profession:</b> {person.profession}
        </li>
        <li>
          <b>Awards: {person.awards.length} </b>
          ({person.awards.join(', ')})
        </li>
        <li>
          <b>Discovered: </b>
          {person.discovery}
        </li>
      </ul>
    </section>
  )
}

export default function Gallery() {
  return (
    <div>
      <h1>Notable Scientists</h1>
      <Profile person={{
        imageId: 'szV5sdG',
        name: 'Maria Skłodowska-Curie',
        profession: 'physicist and chemist',
        discovery: 'polonium (chemical element)',
        awards: [
          'Nobel Prize in Physics',
          'Nobel Prize in Chemistry',
          'Davy Medal',
          'Matteucci Medal'
        ],
      }} />
      <Profile person={{
        imageId: 'YfeOqp2',
        name: 'Katsuko Saruhashi',
        profession: 'geochemist',
        discovery: 'a method for measuring carbon dioxide in seawater',
        awards: [
          'Miyake Prize for geochemistry',
          'Tanaka Prize'
        ],
      }} />
    </div>
  );
}
```

```js src/utils.js
export function getImageUrl(person, size = 's') {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    size +
    '.jpg'
  );
}
```

```css
.avatar { margin: 5px; border-radius: 50%; min-height: 70px; }
.profile {
  border: 1px solid #aaa;
  border-radius: 6px;
  margin-top: 20px;
  padding: 10px;
}
h1, h2 { margin: 5px; }
h1 { margin-bottom: 10px; }
ul { padding: 0px 10px 0px 20px; }
li { margin: 5px; }
```

</Sandpack>

మీరు JSX లక్షణాలు సమాహారం కాకుండా జావాస్క్రిప్ట్ ఆబ్జెక్ట్ యొక్క లక్షణాలను వివరిస్తున్నందున వాక్యనిర్మాణం కొద్దిగా భిన్నంగా కనిపిస్తున్నప్పటికీ, ఈ ఉదాహరణలు చాలా వరకు సమానంగా ఉంటాయి మరియు మీరు ఈ రెండు విధానాలలో ఏదైనా ఎంచుకోవచ్చు.

</Solution>

#### Prop ఆధారంగా ఇమేజ్ సైజ్ అడ్జస్ట్ చేయండి {/*adjust-the-image-size-based-on-a-prop*/}

ఈ ఉదాహరణలో, `Avatar` నెంబర్ గా ఉన్న `size` prop స్వీకరిస్తుంది, ఇది `<img>` యొక్క వెడల్పు మరియు ఎత్తు నిర్ణయిస్తుంది. ఈ ఉదాహరణలో `size` prop విలువ `40` గా నిర్ణయించబడింది. అయితే, మీరు ఇమేజ్ కొత్త ట్యాబ్‌లో తెరిస్తే, మీరు గమనించవచ్చు ఇమేజ్ తేలికగా పెద్దదిగా ఉంటుంది (`160` పిక్సెల్స్). వాస్తవ ఇమేజ్ పరిమాణం మీరు కోరిన థంబ్నెయిల్ పరిమాణం ఆధారంగా నిర్ణయించబడుతుంది.

`Avatar` కంపోనెంట్‌ను `size` prop ఆధారంగా సన్నిహితమైన ఇమేజ్ పరిమాణాన్ని కోరేందుకు మార్చండి. ప్రత్యేకంగా, `size` విలువ `90` కంటే తక్కువ అయితే, `'s'` (''స్మాల్'') ను `'b'` (''బిగ్'') కంటే `getImageUrl` ఫంక్షన్‌కు పంపండి. మీరు చేసిన మార్పులు పని చేస్తున్నాయో లేదో ధృవీకరించడానికి వివిధ `size` prop విలువలతో అవతార్‌లను రెండర్ చేసి, చిత్రాలను కొత్త టాబ్‌లో ఓపెన్ చేయండి.

<Sandpack>

```js src/App.js
import { getImageUrl } from './utils.js';

function Avatar({ person, size }) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person, 'b')}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

export default function Profile() {
  return (
    <Avatar
      size={40}
      person={{ 
        name: 'Gregorio Y. Zara', 
        imageId: '7vQD0fP'
      }}
    />
  );
}
```

```js src/utils.js
export function getImageUrl(person, size) {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    size +
    '.jpg'
  );
}
```

```css
.avatar { margin: 20px; border-radius: 50%; }
```

</Sandpack>

<Solution>

ఇక్కడ మీరు దీన్ని ఎలా చేయగలరో చూపిస్తాను:

<Sandpack>

```js src/App.js
import { getImageUrl } from './utils.js';

function Avatar({ person, size }) {
  let thumbnailSize = 's';
  if (size > 90) {
    thumbnailSize = 'b';
  }
  return (
    <img
      className="avatar"
      src={getImageUrl(person, thumbnailSize)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

export default function Profile() {
  return (
    <>
      <Avatar
        size={40}
        person={{ 
          name: 'Gregorio Y. Zara', 
          imageId: '7vQD0fP'
        }}
      />
      <Avatar
        size={120}
        person={{ 
          name: 'Gregorio Y. Zara', 
          imageId: '7vQD0fP'
        }}
      />
    </>
  );
}
```

```js src/utils.js
export function getImageUrl(person, size) {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    size +
    '.jpg'
  );
}
```

```css
.avatar { margin: 20px; border-radius: 50%; }
```

</Sandpack>

మీరు [`window.devicePixelRatio`](https://developer.mozilla.org/en-US/docs/Web/API/Window/devicePixelRatio) ను పరిగణనలోకి తీసుకుని, అధిక DPI స్క్రీన్ల కోసం మరింత స్పష్టమైన చిత్రం చూపించవచ్చు:

<Sandpack>

```js src/App.js
import { getImageUrl } from './utils.js';

const ratio = window.devicePixelRatio;

function Avatar({ person, size }) {
  let thumbnailSize = 's';
  if (size * ratio > 90) {
    thumbnailSize = 'b';
  }
  return (
    <img
      className="avatar"
      src={getImageUrl(person, thumbnailSize)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

export default function Profile() {
  return (
    <>
      <Avatar
        size={40}
        person={{ 
          name: 'Gregorio Y. Zara', 
          imageId: '7vQD0fP'
        }}
      />
      <Avatar
        size={70}
        person={{ 
          name: 'Gregorio Y. Zara', 
          imageId: '7vQD0fP'
        }}
      />
      <Avatar
        size={120}
        person={{ 
          name: 'Gregorio Y. Zara', 
          imageId: '7vQD0fP'
        }}
      />
    </>
  );
}
```

```js src/utils.js
export function getImageUrl(person, size) {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    size +
    '.jpg'
  );
}
```

```css
.avatar { margin: 20px; border-radius: 50%; }
```

</Sandpack>

Props మీరు ఈ తరహా లాజిక్‌ను `Avatar` కంపోనెంట్ లోపల ఎంకాప్‌ ఎన్‌క్యాప్సులేట్ అనుమతిస్తాయి (కానీ అవసరమైతే తర్వాత మార్పులు చేయవచ్చు), తద్వారా ప్రతి ఒక్కరూ `<Avatar>` కంపోనెంట్‌ని ఉపయోగించడానికి, చిత్రాలను ఎలా అభ్యర్థించాలి మరియు సైజు మార్చాలి అనే దానిపై ఆలోచించకుండానే ఉపయోగించవచ్చు.

</Solution>

#### పాసింగ్ JSX ఇన్ ఏ `children` prop {/*passing-jsx-in-a-children-prop*/}

కింద ఇచ్చిన మార్కప్ నుండి `Card` కంపోనెంట్ ను ఎక్స్‌ట్రాక్ట్ చేసి, దానిలో డిఫరెంట్ JSX ని పంపించడానికి `children` prop ఉపయోగించండి:

<Sandpack>

```js
export default function Profile() {
  return (
    <div>
      <div className="card">
        <div className="card-content">
          <h1>Photo</h1>
          <img
            className="avatar"
            src="https://i.imgur.com/OKS67lhm.jpg"
            alt="Aklilu Lemma"
            width={70}
            height={70}
          />
        </div>
      </div>
      <div className="card">
        <div className="card-content">
          <h1>About</h1>
          <p>Aklilu Lemma was a distinguished Ethiopian scientist who discovered a natural treatment to schistosomiasis.</p>
        </div>
      </div>
    </div>
  );
}
```

```css
.card {
  width: fit-content;
  margin: 20px;
  padding: 20px;
  border: 1px solid #aaa;
  border-radius: 20px;
  background: #fff;
}
.card-content {
  text-align: center;
}
.avatar {
  margin: 10px;
  border-radius: 50%;
}
h1 {
  margin: 5px;
  padding: 0;
  font-size: 24px;
}
```

</Sandpack>

<Hint>

మీరు ఒక కంపోనెంట్ ట్యాగ్‌లో పెట్టిన ఏ JSX. ఆ కంపోనెంట్‌కు `children` prop పంపబడుతుంది.

</Hint>

<Solution>

ఈ విధంగా మీరు రెండు ప్రదేశాలలో `Card` కాంపోనెంట్‌ని ఉపయోగించవచ్చు:

<Sandpack>

```js
function Card({ children }) {
  return (
    <div className="card">
      <div className="card-content">
        {children}
      </div>
    </div>
  );
}

export default function Profile() {
  return (
    <div>
      <Card>
        <h1>Photo</h1>
        <img
          className="avatar"
          src="https://i.imgur.com/OKS67lhm.jpg"
          alt="Aklilu Lemma"
          width={100}
          height={100}
        />
      </Card>
      <Card>
        <h1>About</h1>
        <p>Aklilu Lemma was a distinguished Ethiopian scientist who discovered a natural treatment to schistosomiasis.</p>
      </Card>
    </div>
  );
}
```

```css
.card {
  width: fit-content;
  margin: 20px;
  padding: 20px;
  border: 1px solid #aaa;
  border-radius: 20px;
  background: #fff;
}
.card-content {
  text-align: center;
}
.avatar {
  margin: 10px;
  border-radius: 50%;
}
h1 {
  margin: 5px;
  padding: 0;
  font-size: 24px;
}
```

</Sandpack>

మీరు ప్రతి `Card` కి ఎల్లప్పుడూ టైటిల్ ఉండాలని కోరుకుంటే మీరు `title`ని ప్రత్యేక prop కూడా చేయవచ్చు:

<Sandpack>

```js
function Card({ children, title }) {
  return (
    <div className="card">
      <div className="card-content">
        <h1>{title}</h1>
        {children}
      </div>
    </div>
  );
}

export default function Profile() {
  return (
    <div>
      <Card title="Photo">
        <img
          className="avatar"
          src="https://i.imgur.com/OKS67lhm.jpg"
          alt="Aklilu Lemma"
          width={100}
          height={100}
        />
      </Card>
      <Card title="About">
        <p>Aklilu Lemma was a distinguished Ethiopian scientist who discovered a natural treatment to schistosomiasis.</p>
      </Card>
    </div>
  );
}
```

```css
.card {
  width: fit-content;
  margin: 20px;
  padding: 20px;
  border: 1px solid #aaa;
  border-radius: 20px;
  background: #fff;
}
.card-content {
  text-align: center;
}
.avatar {
  margin: 10px;
  border-radius: 50%;
}
h1 {
  margin: 5px;
  padding: 0;
  font-size: 24px;
}
```

</Sandpack>

</Solution>

</Challenges>
