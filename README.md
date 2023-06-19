# custom-css

## INTRO
I setup this repository to help users of VS Code who hate the warnings on CSS porperties and at-rules that have so-so browser support. While you can add CSS properties in **Settings>CSS>Lint: Valid Properties**, it is not quite right, as it merely ignores the "errors;" at-rules, however, cannot just be added to the linter like properties can.

As of the time of the creation of this file (June 18, 2023 13:40ish US EDT), the CSS **@container** and its related properties (**container**, **container-type**, and **container-name**) have over 80% browser support per [Can I Use](https://caniuse.com) in all major browsers, both desktop and mobile. I was getting annoyed that VS Code was warning me that these properties did not exist, when clearly they've been around for quite a while. I spent days trying to figure out a way to tell the stupid thing that these rules were okay. I kept hoping against hope that the next Code update (which seemed to be coming every other day in the last few weeks) would finally add these rules, but I guess the developer(s) wait till browser support is over 90%... it would be the only thing that makes sense to me.

After many days of fruitless searching (I suck at searching), I finally stumbled accross a post on [Stack Overflow](https://stackoverflow.com/questions/76125833/container-type-property-and-container-rule-are-not-recognized-by-vs-code/76125894#76125894), where the user had asked how to fix this. A user by the name of [starball](https://stackoverflow.com/users/11107541/starball) gave the answer I was looking for, and was the inspiration for this repository.

I created the **custom-css.json** file to support the container at-rule and related properties. This file can be expanded to add support for other properties not yet added to Code's native lint.

## How to use
1. Download the `.vscode` folder and place it in your workspace folder. The '.' before the folder name makes it hidden in Linux distributions. Your workspace folder is the one where your project's files are. For example, you have a file named 'myproject.html' in a folder called 'my_project,' then your workspace folder is 'my_project.'
2. Launch/Relaunch VS Code.

## How to add more stuff
If there are other properties or at-rules you want to add, just follow the pattern of the file. If you want to add another at-rule for example, find the `atDirectives` section and add a new object to the list. The original `atDirectives` should look like this:
```
"atDirectives": [{
          "name": "@container",
          "description": {
               "kind": "markdown",
               "value":"The **@container** CSS at-rule is a conditional group rule that applies styles to a containment context."},
          "references": [{
               "name": "MDN reference",
               "url": "https://developer.mozilla.org/en-US/docs/Web/CSS/@container" 
          }],
          "browsers": ["E105","FF110","C105","S16.0","O91"]
          }],
```
If you wanted to add another at-rule (call it myAtRule), then it would look something like this:
```
"atDirectives": [{
          "name": "@container",
          "description": {
               "kind": "markdown",
               "value":"The **@container** CSS at-rule is a conditional group rule that applies styles to a containment context."},
          "references": [{
               "name": "MDN reference",
               "url": "https://developer.mozilla.org/en-US/docs/Web/CSS/@container" 
          }],
          "browsers": ["E105","FF110","C105","S16.0","O91"]
          }, //<-- add a coma, then add a new object using curly brackets {} 
          {
          "name": "@myAtRule",
          "description": "Simple description of myAtRule. If you want to use markdown, follow the pattern of the description above."
          "references": [{
                "name": "Title of your reference"
                "url": "https://linktoreference"
          }],
          "browsers": []
          }]
```

The same process applies to the `properties` section. Forgive my tabbing inconsitency above, please.

The only "fields" that are required are *name* and *description*, the rest are optional. If you are editing the file in VS Code, you will notice that the editor will help you, and give you warnings if you are entering invalid values in the directives. This is because of the "$schema" line at the begining of the file. VS Code will try to guide you along when adding new properties to the file. You can also download the [schema file](https://raw.githubusercontent.com/microsoft/vscode-css-languageservice/master/docs/customData.schema.json) so you can look at the entire stucture (you can actually add pseudo-classes, as well as include the status of the property you are adding). 

## Drawbacks
There are a couple drawbacks to using this method, none of which are really material, but can be a bit annoying if you suffer even from a minor case of OCD.
1. The ability to add a "Syntax" example line seems to be missing from the schema (unless it is part of the description and I'm just stupid).
2. This one can be more annoying, but still does not affect much: properties inside a custom at-rule do not call the reference box when you hover over them.

## Final thoughts
I placed this on gitHub with the hope that someone smarter than me will look it over, fork it, and make it better. I hope this helps you as much as starball's answer helped me.
