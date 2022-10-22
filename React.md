# React helper

## forms
button inside form execute onSubmit, default behaviour - refresh.
Use event.preventDefault()

``` jsx
<form onSubmit={handleSubmit} className={styles.newTaskForm}>
        <input
          placeholder="add a new task"
          value={title}
          type="text"
          onChange={onChangeTitle}
        />
        <button>
          Create
          <AiOutlinePlusCircle size={20} />
        </button>
      </form>
```

this refreshes, **BAD**
``` jsx
 const handleSubmit = () => {
    onAddTask(title);
  };
```

**Good one**

``` JSX
 const handleSubmit = (event) => {
    event.preventDefault()
    onAddTask(title);
  };
```

## [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

`filter()` calls a provided `callbackFn` function once for each element in an array, and constructs a new array of all the values for which `callbackFn` returns [a value that coerces to `true`](https://developer.mozilla.org/en-US/docs/Glossary/Truthy). Array elements which do not pass the `callbackFn` test are skipped, and are not included in the new array.

``` js
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]

```

```js 
function isBigEnough(value) {
  return value >= 10;
}

const filtered = [12, 5, 8, 130, 44].filter(isBigEnough);
// filtered is [12, 130, 44]

```

``` jsx
const completedTasks = tasks.filter(task=> task.isCompleted).length;
```

## Local storage
(string, string)
``` jsx
  const LOCAL_STORAGE_KEY = "todo:savedtasks";


  const setTasksAndSave = (newTasks) => {
    setTasks(newTasks);
    localStorage.setItem(LOCAL_STORAGE_KEY, JSON.stringify(newTasks));
  };


  const loadSavedTasks = () => {
    const saved = localStorage.getItem(LOCAL_STORAGE_KEY);
    // console.log(saved);
    if (saved) {
      setTasks(JSON.parse(saved));
    }
  };


  useEffect(() => {
    loadSavedTasks();
  }, []); //Empty dep array => executes once onLoad
```

## Images import from folder

``` jsx
//icons.js
 export const file1 = require("./IconRed_100x100.png");
 export const file2 = require("./IconSilver_100x100.png");
 export const file3 = require("./IconWhite_100x100.png");
 export const file4 = require("./IconBrown1_100x100.png");
 export const file5 = require("./IconBrown2_100x100.png");
 export const file6 = require("./IconGray_100x100.png");
 export const file7 = require("./IconMetallic_100x100.png");
 export const file8 = require("./IconMetallic_100x100.png");
 export const file9 = require("./IconMetallic_100x100.png");
 export const file10 = require("./IconMetallic_100x100.png");
```

```jsx
import * as ALL from "../assets/png/icons";

 const itemsToRender = [];
 for (let x in ALL) {
  console.log(x);
  itemsToRender.push(
    <div key={x} className="image-gallery-item">
     <img src={ALL[x]}></img>
    </div>
  );
 }

 function ImageGallery() {
 return (
   <>
    <div className="image-gallery">{itemsToRender}</div>
   </>
  );
 }

 export default ImageGallery;
```
