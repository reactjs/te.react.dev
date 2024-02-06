---
title: ఎడిటర్ సెటప్
---

<Intro>

మీ ఎడిటర్‌ని ప్రొపెర్గా కాన్ఫిగర్ చేయడం వలన మీ కోడ్ ను సులభంగా చదవచ్చు మరియు వేగంగా కూడా వ్రాయవచ్చు. అదనంగా, మీరు కోడ్ను వ్రాస్తున్నప్పుడు బగ్‌లను గుర్తించడంలో ఇది మీకు సహాయపడుతుంది! మీరు ఎడిటర్‌ని సెటప్ చేయడం ఇదే మొదటిసారి అయితే లేదా మీరు మీ ప్రస్తుత ఎడిటర్‌ని ట్యూన్ అప్ చేయాలని అనుకొంటే, మేము వీటిని సిఫార్సు చేస్తాము.

</Intro>

<YouWillLearn>

* అత్యంత ప్రజాదరణ పొందిన ఎడిటర్లు ఏమిటి
* మీ కోడ్‌ను ఆటోమేటిక్ గా ఎలా ఫార్మాట్ చేయాలి

</YouWillLearn>

## మీ ఎడిటర్ {/*your-editor*/}

నేడు వాడుకలో ఉన్న అత్యంత ప్రజాదరణ పొందిన ఎడిటర్లలో [VS Code](https://code.visualstudio.com/) ఒకటి. ఇది ఎక్సటెన్షన్స్ యొక్క పెద్ద మార్కెట్‌ప్లేస్‌ను కలిగి ఉంది మరియు GitHub వంటి పాపులర్ సర్వీసులతో బాగా ఇంటిగ్రేట్ అవుతుంది. దిగువ జాబితా చేయబడిన చాలా ఫీచర్లను VS Code కి ఎక్సటెన్షన్స్ లాగా కూడా జోడించవచ్చు, తద్వారా దీన్ని చాలా వరకు కాన్ఫిగర్ చేయవచ్చు!

React కమ్యూనిటీలో ఉపయోగించే ఇతర పాపులర్ టెక్స్ట్ ఎడిటర్‌లు:

* [WebStorm](https://www.jetbrains.com/webstorm/) అనేది JavaScript కోసం ప్రత్యేకంగా రూపొందించబడిన ఇంటిగ్రేటెడ్ డెవలప్మెంట్ ఎన్విరాన్మెంట్.
* [Sublime Text](https://www.sublimetext.com/) ‌లో JSX మరియు TypeScript కోసం [సింటాక్స్ హైలైటింగ్](https://stackoverflow.com/a/70960574/458193) మరియు ఆటోకంప్లీట్ ఫీచర్లకు బిల్ట్ ఇన్ సపోర్ట్ ఉంది.
* [Vim](https://www.vim.org/) అనేది అత్యంత కాన్ఫిగర్ చేయగల టెక్స్ట్ ఎడిటర్, ఇది ఎలాంటి టెక్స్ట్‌ని అయినా సృష్టించడం మరియు మార్చడం చాలా ఎఫిసియెంట్గా చేయడానికి నిర్మించబడింది. ఇది చాలా UNIX సిస్టమ్‌లతో మరియు Apple OS X తో "vi" గా ఇంక్లూడ్ చేయబడింది.

## Recommended text editor features {/*recommended-text-editor-features*/}

Some editors come with these features built in, but others might require adding an extension. Check to see what support your editor of choice provides to be sure!

### Linting {/*linting*/}

Code linters find problems in your code as you write, helping you fix them early. [ESLint](https://eslint.org/) is a popular, open source linter for JavaScript. 

* [Install ESLint with the recommended configuration for React](https://www.npmjs.com/package/eslint-config-react-app) (be sure you have [Node installed!](https://nodejs.org/en/download/current/))
* [Integrate ESLint in VSCode with the official extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

**Make sure that you've enabled all the [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks) rules for your project.** They are essential and catch the most severe bugs early. The recommended [`eslint-config-react-app`](https://www.npmjs.com/package/eslint-config-react-app) preset already includes them.

### Formatting {/*formatting*/}

The last thing you want to do when sharing your code with another contributor is get into an discussion about [tabs vs spaces](https://www.google.com/search?q=tabs+vs+spaces)! Fortunately, [Prettier](https://prettier.io/) will clean up your code by reformatting it to conform to preset, configurable rules. Run Prettier, and all your tabs will be converted to spaces—and your indentation, quotes, etc will also all be changed to conform to the configuration. In the ideal setup, Prettier will run when you save your file, quickly making these edits for you.

You can install the [Prettier extension in VSCode](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) by following these steps:

1. Launch VS Code
2. Use Quick Open (press Ctrl/Cmd+P)
3. Paste in `ext install esbenp.prettier-vscode`
4. Press Enter

#### Formatting on save {/*formatting-on-save*/}

Ideally, you should format your code on every save. VS Code has settings for this!

1. In VS Code, press `CTRL/CMD + SHIFT + P`.
2. Type "settings"
3. Hit Enter
4. In the search bar, type "format on save"
5. Be sure the "format on save" option is ticked!

> If your ESLint preset has formatting rules, they may conflict with Prettier. We recommend disabling all formatting rules in your ESLint preset using [`eslint-config-prettier`](https://github.com/prettier/eslint-config-prettier) so that ESLint is *only* used for catching logical mistakes. If you want to enforce that files are formatted before a pull request is merged, use [`prettier --check`](https://prettier.io/docs/en/cli.html#--check) for your continuous integration.
