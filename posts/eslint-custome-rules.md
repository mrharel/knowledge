# Creating your own custome ESLint rule

Sometimes you want to enforce some JS linting rules which are only specific to you and your team. Here I will show how to do this on a local mode. 

For this example i will create a rule that will check that logical expressions with React components break into a new line. For example
the following is not ok:

```javascript
render() {
  return (
    <div>
      {condition1 && <UserPic />}
    </div>
  );
}
```

but it should be like this:

```javascript
render() {
  return (
    <div>
      {condition1 && 
        <UserPic />
      }
    </div>
  );
}
```

## Implementation
- Create a local folder for your rules. in our case `my-eslint-test`
- Inside that folder create a file called `my-test.js`
- Paste the following into this file:

```javascript
module.exports = function(context) {
  return {
    LogicalExpression: function(node) {
      if (node.operator === '&&' &&
          node.right.type === 'JSXElement' &&
          node.left.type === 'MemberExpression'&&
          node.right.loc.start.line === node.left.loc.start.line) {
          context.report(node, 'React component must starts at a new line in logical expression');
      }
    }
  };
};
```
- Add the rule in the `.eslintrc` file like so:

```javascript
"rules": {     
      "my-test": 2
  }
```

- In `package.json` add the `--rulesdir` options to your lint script like so:

```javascript
"scripts": {    
    "lint": "eslint --rulesdir my-eslint-plugin/ components",
```

That is it. Once you will to `npm run lint` your rule will be executed in the task. 

ESLint create a node tree from the code, and in order to write new rules it is better to understand that and to know about all the 
options of nodes. You can checkout some more info [here](https://github.com/estree/estree).

## Resources
- [Writing Your Own Eslint Rules](https://worstgenerationengineers.ghost.io/2016/05/07/writing-your-own-eslint-rules/)
- [--rulesdir](http://eslint.org/docs/user-guide/command-line-interface#rulesdir)
- [Writing custom EsLint rules](https://www.kenneth-truyers.net/2016/05/27/writing-custom-eslint-rules/)
