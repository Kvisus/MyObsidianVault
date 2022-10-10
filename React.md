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