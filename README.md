# plugin-enterprise-compatibility.js

> Octokit plugin for improving GHE compatibility

The GitHub API teams is continuously improving existing APIs to make the overall platform more consistent. For example, the [Add labels to an issue](https://developer.github.com/v3/issues/labels/#add-labels-to-an-issue) expected the label names array to be sent directly in the request body root, as you can still see in the documentation for [GHE 2.15](https://developer.github.com/enterprise/2.15/v3/issues/labels/#input).

While consistency is great, changing like the above makes the current `octokit.issues.addLabels()` incompatible with GHE v2.15 and older. If you require compatibility with GHE versions, you can use the [Enterprise rest plugin](https://github.com/octokit/plugin-enterprise-rest.js), but that will remove new endpoint methods that are not available on Enterprise yet.

As a compromise, this plugin is reverting changes such as the one above to remain compatible with currently supported GitHub enterprise versions.

## Usage

```js
const Octokit = require('@octokit/rest')
  .plugin(require('@octokit/enterprise-compatibility'))
const octokit = new Octokit()

octokit.auth({
  type: 'token',
  token: GITHUB_TOKEN
})

octokit.issues.addLabels({ owner, repo, number, labels: ['foo', 'bar'] })
// sends ["foo", "bar"] instead of {"labels":["foo", "bar"]}
```

## LICENSE

[MIT](LICENSE)
