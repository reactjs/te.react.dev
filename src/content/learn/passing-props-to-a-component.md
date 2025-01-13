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

It is common to nest built-in browser tags:

```js
<div>
  <img />
</div>
```

Sometimes you'll want to nest your own components the same way:

```js
<Card>
  <Avatar />
</Card>
```

When you nest content inside a JSX tag, the parent component will receive that content in a prop called `children`. For example, the `Card` component below will receive a `children` prop set to `<Avatar />` and render it in a wrapper div:

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

Try replacing the `<Avatar>` inside `<Card>` with some text to see how the `Card` component can wrap any nested content. It doesn't need to "know" what's being rendered inside of it. You will see this flexible pattern in many places.

You can think of a component with a `children` prop as having a "hole" that can be "filled in" by its parent components with arbitrary JSX. You will often use the `children` prop for visual wrappers: panels, grids, etc.

<Illustration src="/images/docs/illustrations/i_children-prop.png" alt='A puzzle-like Card tile with a slot for "children" pieces like text and Avatar' />

## How props change over time {/*how-props-change-over-time*/}

The `Clock` component below receives two props from its parent component: `color` and `time`. (The parent component's code is omitted because it uses [state](/learn/state-a-components-memory), which we won't dive into just yet.)

Try changing the color in the select box below:

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

This example illustrates that **a component may receive different props over time.** Props are not always static! Here, the `time` prop changes every second, and the `color` prop changes when you select another color. Props reflect a component's data at any point in time, rather than only in the beginning.

However, props are [immutable](https://en.wikipedia.org/wiki/Immutable_object)—a term from computer science meaning "unchangeable". When a component needs to change its props (for example, in response to a user interaction or new data), it will have to "ask" its parent component to pass it _different props_—a new object! Its old props will then be cast aside, and eventually the JavaScript engine will reclaim the memory taken by them.

**Don't try to "change props".** When you need to respond to the user input (like changing the selected color), you will need to "set state", which you can learn about in [State: A Component's Memory.](/learn/state-a-components-memory)

<Recap>

* To pass props, add them to the JSX, just like you would with HTML attributes.
* To read props, use the `function Avatar({ person, size })` destructuring syntax.
* You can specify a default value like `size = 100`, which is used for missing and `undefined` props.
* You can forward all props with `<Avatar {...props} />` JSX spread syntax, but don't overuse it!
* Nested JSX like `<Card><Avatar /></Card>` will appear as `Card` component's `children` prop.
* Props are read-only snapshots in time: every render receives a new version of props.
* You can't change props. When you need interactivity, you'll need to set state.

</Recap>



<Challenges>

#### Extract a component {/*extract-a-component*/}

This `Gallery` component contains some very similar markup for two profiles. Extract a `Profile` component out of it to reduce the duplication. You'll need to choose what props to pass to it.

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

Start by extracting the markup for one of the scientists. Then find the pieces that don't match it in the second example, and make them configurable by props.

</Hint>

<Solution>

In this solution, the `Profile` component accepts multiple props: `imageId` (a string), `name` (a string), `profession` (a string), `awards` (an array of strings), `discovery` (a string), and `imageSize` (a number).

Note that the `imageSize` prop has a default value, which is why we don't pass it to the component.

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

Note how you don't need a separate `awardCount` prop if `awards` is an array. Then you can use `awards.length` to count the number of awards. Remember that props can take any values, and that includes arrays too!

Another solution, which is more similar to the earlier examples on this page, is to group all information about a person in a single object, and pass that object as one prop:

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

Although the syntax looks slightly different because you're describing properties of a JavaScript object rather than a collection of JSX attributes, these examples are mostly equivalent, and you can pick either approach.

</Solution>

#### Adjust the image size based on a prop {/*adjust-the-image-size-based-on-a-prop*/}

In this example, `Avatar` receives a numeric `size` prop which determines the `<img>` width and height. The `size` prop is set to `40` in this example. However, if you open the image in a new tab, you'll notice that the image itself is larger (`160` pixels). The real image size is determined by which thumbnail size you're requesting.

Change the `Avatar` component to request the closest image size based on the `size` prop. Specifically, if the `size` is less than `90`, pass `'s'` ("small") rather than `'b'` ("big") to the `getImageUrl` function. Verify that your changes work by rendering avatars with different values of the `size` prop and opening images in a new tab.

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

Here is how you could go about it:

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

You could also show a sharper image for high DPI screens by taking [`window.devicePixelRatio`](https://developer.mozilla.org/en-US/docs/Web/API/Window/devicePixelRatio) into account:

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

Props let you encapsulate logic like this inside the `Avatar` component (and change it later if needed) so that everyone can use the `<Avatar>` component without thinking about how the images are requested and resized.

</Solution>

#### Passing JSX in a `children` prop {/*passing-jsx-in-a-children-prop*/}

Extract a `Card` component from the markup below, and use the `children` prop to pass different JSX to it:

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

Any JSX you put inside of a component's tag will be passed as the `children` prop to that component.

</Hint>

<Solution>

This is how you can use the `Card` component in both places:

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

You can also make `title` a separate prop if you want every `Card` to always have a title:

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
