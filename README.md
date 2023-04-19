# extracting-json-from-string
(Simple!) Extracting JSON from String ✨

```js
async function extractJSON(str) {
    return await new Promise((resolve) => {
        let data = str;
        try {
            if (typeof data === 'string') {
                data = JSON.parse(str);
            }
        } catch (e) {
            try {
                const jsonStart = str.indexOf("{");
                const jsonEnd = str.lastIndexOf("}");
                const jsonString = str.slice(jsonStart, jsonEnd + 1);
                resolve(JSON.parse(jsonString));
            } catch (e) {
                console.log(e)
                resolve(false)
            }
        }
        resolve(data);
    });
}

extractJSON('demo string {"text": "hi!"}'); // result: {"text": "hi!"}
extractJSON({"text": "hi!"}); // result: {"text": "hi!"}
extractJSON("hello"); // result: false;
```
