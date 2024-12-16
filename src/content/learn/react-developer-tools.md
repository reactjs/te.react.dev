---
title: React డెవలపర్ టూల్స్
---

<Intro>

React [కాంపోనెంట్‌లను](/learn/your-first-component) తనిఖీ చేయడానికి, [props](/learn/passing-props-to-a-component) మరియు [state](/learn/state-a-components-memory) ని ఎడిట్ చేయడానికి మరియు పెర్ఫార్మన్స్ సమస్యలను గుర్తించడానికి React డెవలపర్ టూల్స్ ను ఉపయోగించండి.

</Intro>

<YouWillLearn>

* React డెవలపర్ టూల్స్ ను ఎలా ఇన్‌స్టాల్ చేయాలి

</YouWillLearn>

## బ్రౌజర్ ఎక్సటెన్షన్ {/*browser-extension*/}

React తో నిర్మించిన వెబ్‌సైట్‌లను డీబగ్ చేయడానికి సులభమైన మార్గం React డెవలపర్ టూల్స్ బ్రౌజర్ ఎక్సటెన్షన్ ను ఇన్‌స్టాల్ చేయడం. ఇది అనేక ప్రసిద్ధ బ్రౌజర్‌లకు అందుబాటులో ఉంది:

* [**Chrome** కోసం ఇన్‌స్టాల్ చేయండి](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
* [**Firefox** కోసం ఇన్‌స్టాల్ చేయండి](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)
* [**Edge** కోసం ఇన్‌స్టాల్ చేయండి](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil)

ఇప్పుడు, మీరు **React తో నిర్మించిన వెబ్‌సైట్‌** ను సందర్శిస్తే, మీరు _Components_ మరియు _Profiler_ ప్యానెల్‌లను చూస్తారు.

![React డెవలపర్ టూల్స్ ఎక్స్టెన్షన్](/images/docs/react-devtools-extension.png)

### Safari మరియు ఇతర బ్రౌజర్‌లు {/*safari-and-other-browsers*/}
ఇతర బ్రౌజర్‌ల కోసం (ఉదాహరణకు, Safari), [`react-devtools`](https://www.npmjs.com/package/react-devtools) npm ప్యాకేజీని ఇన్‌స్టాల్ చేయండి:
```bash
# Yarn
yarn global add react-devtools

# Npm
npm install -g react-devtools
```

తరువాత టెర్మినల్ నుండి డెవలపర్ టూల్స్ ను ఓపెన్ చేయండి:
```bash
react-devtools
```

ఆపై మీ వెబ్‌సైట్ యొక్క `<head>` ప్రారంభంలో క్రింది `<script>` ట్యాగ్‌ని జోడించడం ద్వారా మీ వెబ్‌సైట్‌ను కనెక్ట్ చేయండి:
```html {3}
<html>
  <head>
    <script src="http://localhost:8097"></script>
```

ఇప్పుడు మీ బ్రౌజర్‌లో వెబ్‌సైట్‌ను రీలోడ్ చేయండి, తద్వారా మీరు దీన్ని డెవలపర్ టూల్స్ లో వీక్షించవచ్చు.

![React డెవలపర్ టూల్స్ స్టాండ్ అలొనె](/images/docs/react-devtools-standalone.png)

## మొబైల్ (React Native) {/*mobile-react-native*/}

[React Native](https://reactnative.dev/)‌ తో రూపొందించబడిన యాప్‌లను తనిఖీ చేయడానికి, మీరు React డెవలపర్ టూల్స్‌ను లోతుగా అనుసంధానించే ఇన్-బిల్ట్ డీబగ్గర్ అయిన [React Native DevTools](https://reactnative.dev/docs/debugging/react-native-devtools) ని ఉపయోగించవచ్చు. అన్ని ఫీచర్లు బ్రౌజర్ ఎక్స్టెన్షన్ తో సమానంగా పని చేస్తాయి, నేటివ్ ఎలిమెంట్ హైలైటింగ్ మరియు సెలక్షన్ తో సహా.

[React Native డీబగ్గింగ్ గురించి మరింత తెలుసుకోండి.](https://reactnative.dev/docs/debugging)

> 0.76 కంటే ముందు React Native వెర్షన్‌ల కోసం, దయచేసి పైన ఉన్న [Safari మరియు ఇతర బ్రౌజర్‌ల](#safari-and-other-browsers) గైడ్‌ని అనుసరించడం ద్వారా React DevTools యొక్క స్టాండ్ అలొనె బిల్డ్ ను ఉపయోగించండి.
