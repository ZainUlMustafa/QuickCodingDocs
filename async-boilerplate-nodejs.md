## Async Boilerplate for Testing NodeJS

```
async function processing() {
    sleep(500, function () { });
}

function sleep(time, callback) {
    var stop = new Date().getTime();
    while (new Date().getTime() < stop + time);
    callback();
}

async function main() {
    try {
        await processing()
    } catch (err) {
        console.log(err)
    }
}

main();
```
