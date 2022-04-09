## Streams
Streams are the most fundamental Structure when it comes to Stealify code 

```js
// Create a Promise that resolves after ms time
const delayedPromise = (ms) => new Promise((done) => setTimeout(done, ms));

// Generate a Promise that listens only once for an event
// supports eventEmitters that get called with multiple arguments
/** @returns {Promise<[T]>} */
const oncePromise = (emitter, event) => 
  new Promise((resolve) => {
    const handler = (...args) => {
      emitter.removeEventListener(event, handler);
      resolve(args);
    };
    emitter.addEventListener(event, handler);
  });

// Turn any eventEmitter into a stream
const streamify = async function*(event, element) {
  while (true) { yield await oncePromise(element, event); }
};

// Only pass along events that meet a condition
const filter = async function*(stream, test) {
  for await (let event of stream) {
    test(event) && yield event;
  }
};

// Transform every val of the stream
const map = async function*(stream, transform) {
  for await (let val of stream) {
    yield transform(val);
  }
};

// Only pass along event if some time has passed since the last one
const throttle = async function*(stream, delay) {
  let lastTime;
  let thisTime;
  for await (let event of stream) {
    thisTime = (new Date()).getTime();
    if (!lastTime || thisTime - lastTime > delay) {
      lastTime = thisTime;
      yield event;
    }
  }
};

// manly to show that extract is a fn
const identity = (e) => e;

// Only pass along events that differ from the last one
const distinct = async function*(stream, extract = identity) {
  var lastVal;
  var thisVal;
  for await (let event of stream) {
    thisVal = extract(event);
    if (thisVal !== lastVal) {
      lastVal = thisVal;
      yield event;
    }
  }
};

// Invoke a callback every time an event arrives
const subscribe = async (stream, callback) => {
  for await (let event of stream) {
    callback(event);
  }
};

const defferedPromise = () => {
  const handlers = {};
  const promise = new Promise((resolve,reject)=>Object.assig(handlers, { resolve, reject }));
  return Object.assign(promise, handlers);
}

const createEventEmitter = () => {
 
   const callbackMaps = {};
     
   return {
      addEventListner(event, callback) {
        if (!callbackMaps[event]) {
          callbackMaps[event] = new Map();
        }
        callbackMaps[event].set(callback, callback);
      },
      removeEventListner(event, callback) {
        callbackMaps[event].delete(callback);
        if (callbackMaps[event].length === 0) {
          delete callbackMaps[event];
        }
      },
      emit(event, val) {
         if (callbackMaps[event]) {
           callbackMaps[event].forEach(((callback) => callback(val))
         }
      },
   }
}

const tee = (stream) => {
  const source = stream;
  let [promise1,promise2] = [defferedPromise(),defferedPromise()]
  subscribe(stream,() => {}
  return {}
}
```

as everything is async in Stealify it is good to be familar with the most generic stream constructs. They are used to form so called observables so you can see it as your own react vue or similar.
