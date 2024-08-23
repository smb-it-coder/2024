
function uniq(arr){


    let seen = new Set();
    let duplicates = new Set();
    for(let num of arr) {
        if(seen.has(num)) {
            duplicates.add(num)
        } else {
            seen.add(num)
        }
        
    }

    return (Array.from(duplicates)).sort((a,b)=> a-b);
}

console.log(uniq([1,2,4,65,65,65,7,7,3,4,3,5,2,5,2]));



## OR condition

function findDuplicates(arr) {
    const counts = {};
    const duplicates = [];
    
    for (const num of arr) {
        if (counts[num]) {
            if (counts[num] === 1) {
                duplicates.push(num);
            }
            counts[num]++;
        } else {
            counts[num] = 1;
        }
    }
    
    return duplicates;
}

// Example usage:
const numbers = [1, 2, 3, 4, 5, 1, 2, 6, 7];
const result = findDuplicates(numbers);
console.log(result); // Output: [1, 2]
