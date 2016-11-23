# Cycle.js and Reactive Libraries

Meiosis has some inspiration from [Cycle.js](http://cycle.js.org/), by [André Staltz/André Medeiros](http://staltz.com), as well as Reactive Libraries such as [RxJS](http://reactivex.io/rxjs/), [Kefir](https://rpominov.github.io/kefir/), [most](https://github.com/cujojs/most), [Bacon.js](https://baconjs.github.io/), and [Flyd](https://github.com/paldepind/flyd).

While not as deeply entrenched in reactive principles as these reactive libraries, nor as strict about separation of pure code versus side effects as Cycle.js, Meiosis does have a reactive nature in that your code starts a reactive sequence with `propose`, and Meiosis wires everything together so that your functions, `receive`, `view`, and so on, are called and the user interface is refreshed to reflect the changes that took place.
