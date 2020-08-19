# compound-callback-subtree
A subtree method that offers great flexibility and features to the developer.
<pre><code class="language-javascript">npm i compound-callback-subtree

const { compoundCallbackSubTree } = require("compound-callback-subtree");</code></pre>
<h3>compoundCallbackSubTree([options][,callback])</h3>
<ul>
    <li><code>options</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">&lt;Object&gt;</a></li>
    <ul>
        <li><code>basePath</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type">&lt;string&gt;</a> Default: "./"</li>
        <li><code>dirStatsCb</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">&lt;Function&gt;</a> Default: <code>(data, callback) => callback()</code></li>
        <ul>
            <li><code>data</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">&lt;Object&gt;</a></li>
            <ul>
                <li><code>branch</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">&lt;Object&gt;</a></li>
                <li><code>stats</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">&lt;Object&gt;</a></li>
            </ul>
            <li><code>callback</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">&lt;Function&gt;</a></code> Required!</li>
        </ul>
        <li><code>fileStatsCb</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">&lt;Function&gt;</a> Default: <code>(data, callback) => callback()</code></li>
        <ul>
            <li><code>data</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">&lt;Object&gt;</a></li>
            <ul>
                <li><code>branch</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">&lt;Object&gt;</a></li>
                <li><code>stats</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">&lt;Object&gt;</a></li>
            </ul>
            <li><code>callback</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">&lt;Function&gt;</a></code> Required!</li>
        </ul>
        <li><code>subBranchCb</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">&lt;Function&gt;</a> Default: <code>data => new Promise(resolve => resolve())</code></li>
        <ul>
            <li><code>data</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">&lt;Object&gt;</a></li>
            <ul>
                <li><code>path</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type">&lt;string&gt;</a></li>
                <li><code>nextPath</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type">&lt;string&gt;</a></li>
                <li><code>file</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type">&lt;string&gt;</a></li>
                <li><code>branch</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">&lt;Object&gt;</a></li>
            </ul>
            <li>Returns <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise">&lt;Promise&gt;</a></li>
            <ul>
                <li><code>resolve</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve">&lt;Promise.resolve&gt;</a></li>
                <ul>
                    <li><code>nextBranch</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">&lt;Object&gt;</a> | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Undefined_type">&lt;undefined&gt;</a></li>
                </ul>
                <li><code>reject</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject">&lt;Promise.reject&gt;</a></li>
            </ul>
        </ul>
    </ul>
    <li><code>callback</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">&lt;Function&gt;</a> Default: <code>tree => tree</code></li>
    <ul>
        <li><code>tree</code> <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">&lt;Object&gt;</a></li>
    </ul>
</ul>

The function <b>fsStatsTree</b> has been developed to return a data-tree of sub-directories and files in those sub-directories. The function takes in two parameters, you must pass a base-path as the 1st parameter and you may (optionally) pass an Object as 2nd parameter. This function internally calls the <a href="https://nodejs.org/dist/latest-v12.x/docs/api/fs.html#fs_fs_stat_path_options_callback">fs.stat()</a> and the <a href="https://nodejs.org/dist/latest-v12.x/docs/api/fs.html#fs_fs_readdir_path_options_callback">fs.readdir()</a> methods, like every other recursive directory tree. The Object from the 2nd parameter must be given keys from the <a href="https://nodejs.org/dist/latest-v12.x/docs/api/fs.html#fs_class_fs_stats">fs.Stats</a> class and function callbacks as the values. The returned data-tree of this function adds the keys from the <a href="https://nodejs.org/dist/latest-v12.x/docs/api/fs.html#fs_class_fs_stats">fs.Stats</a> class to files-only (not to directories). The callbacks were added because now you may modify the data returned from the keys from the <a href="https://nodejs.org/dist/latest-v12.x/docs/api/fs.html#fs_class_fs_stats">fs.Stats</a> class. This allows you to parse the time returned by the "birthtimeMs"-key through the Date class and return an ISO-string, or to add the String " bytes" to the values returned from the "size"-key, or to do nothing and just return the actual value like the return from the "ctimeMs"-key. As an extra feature you may also pass the callback itself through the function <b>namedStatsCallback</b>. This function takes in the new name as 1st parameter and the callback as the 2nd parameter. It will add a static "name" property to the callback. It allows you to change the naming of the keys from the <a href="https://nodejs.org/dist/latest-v12.x/docs/api/fs.html#fs_class_fs_stats">fs.Stats</a> class into more readable Strings to your liking. For example it changes the key "atimeMs" into the String "last accessed" and changes the "birthtimeMs" into "created".

<pre>root
|__test.js
|__compund-callback-subtree
|     |__ .git.js
|     |     |__ etc...
|     |__ index.js
|     |__ package.json
|     |__ README.md
|__etc...
// ...
const path = require("path");
const { compoundCbSubTree, statCallback } = require("compound-cb-subtree");
const { localeTimezoneDate, dateNotation, utc0 } = require("locale-timezone-date");
// ...
const e3sBytesNotation = function load() {
    const e3sBytes = { 0: "B", 1: "KB", 2: "MG", 3: "GB", 4: "TB", 5: "PB" };
    return byteLength => {
        let e3s = 0;
        while (byteLength >= 1000 && e3sBytes[e3s++])
            byteLength /= 1000;
        return `${byteLength} ${e3sBytes[e3s]}`;
    }
}();
const ignore = { ".git": true, ".gitignore": true };
// ...
compoundCallbackSubTree({
    subBranchCb: branch => new Promise((resolve, reject) => {
        if (!ignore[branch.file])
            resolve({ path: path.join(__dirname, branch.nextPath) });
        reject();
    }),
    dirStatsCbs: (branch, callback) => {
        branch.currentBranch["create-time"] = localeTimezoneDate.toISOString(new Date(branch.stats.birthTimeMs));
        callback();
    },
    fileStatsCbs: (branch, callback) => {
        branch.currentBranch["create-time"] = localeTimezoneDate.toISOString(new Date(branch.stats.birthTimeMs));
        branch.currentBranch["byte-size"] = e3sBytesNotation(branch.stats.size);
        callback();
    }
}, tree => console.log("tree:", tree));
// ...
// returns
// tree: {
//   'create-time': '2020-08-06T21:50:56.504+0200',
//   'compound-cb-subtree': {
//     path: 'D:\\js\\node_modules\\compound-cb-subtree',
//     'create-time': '2020-08-16T23:29:00.675+0200',
//     'index.js': {
//       path: 'D:\\js\\node_modules\\compound-cb-subtree\\index.js',
//       'create-time': '2020-08-16T23:29:02.819+0200',
//       'byte-size': '2.418 KB'
//     },
//     'package.json': {
//       path: 'D:\\js\\node_modules\\compound-cb-subtree\\package.json',
//       'create-time': '2020-08-16T23:29:02.827+0200',
//       'byte-size': '666 B'
//     },
//     'README.md': {
//       path: 'D:\\js\\node_modules\\compound-cb-subtree\\README.md',
//       'create-time': '2020-08-16T23:29:02.813+0200',
//       'byte-size': '3.48 KB'
//     }
//   },
//   // etc...
// }</pre>
