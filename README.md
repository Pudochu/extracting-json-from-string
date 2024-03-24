# extracting-json-from-string
(Simple!) Extracting JSON from String ✨

```js
async function extractJSON(str) {
    // If the input is already an object, return it directly.
    if (typeof str === 'object') {
        return str;
    }

    // If the input is a string, try to parse it as JSON.
    if (typeof str === 'string') {
        try {
            return JSON.parse(str);
        } catch (e) {
            // If the first parse attempt fails, try to find the part that contains a JSON object.
            try {
                const jsonStart = str.indexOf("{");
                const jsonEnd = str.lastIndexOf("}");
                if (jsonStart !== -1 && jsonEnd !== -1) {
                    const jsonString = str.slice(jsonStart, jsonEnd + 1);
                    return JSON.parse(jsonString);
                }
            } catch (e) {
                // If the second parse attempt also fails, return false.
                console.error(e);
                return false;
            }
        }
    }

    // If the input is neither a string nor an object, return false.
    return false;
}

// Sample usages to test the function:
extractJSON('demo string {"text": "hi!"}').then(console.log); // result: {"text": "hi!"}
extractJSON({"text": "hi!"}).then(console.log); // result: {"text": "hi!"}
extractJSON("hello").then(console.log); // result: false;
```
