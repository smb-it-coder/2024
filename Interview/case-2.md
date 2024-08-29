let obj = {
    "name": "test",
    "address": {
        "street": "street",
        "city": "pune",
    }
};

function contains(objects, key) {
    for (let k in objects) {
        if (objects.hasOwnProperty(k)) {
            if (k === key) {
                return true;
            }
            if (typeof objects[k] === 'object' && objects[k] !== null) {
                if (contains(objects[k], key)) {
                    return true;
                }
            }
        }
    }
    return false;
}

console.log(contains(obj, 'city')); // true
console.log(contains(obj, 'zipcode')); // false
