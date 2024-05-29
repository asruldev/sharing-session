
# Curry and Function Composition

![Curry and Composition](https://mccormick.widen.net/content/dch8baa1ad/original/curry_d_agneau_2000x1125.jpg)

**Functional programming** adalah paradigma pemrograman yang menekankan penggunaan **fungsi** dan penghindaran perubahan status (mutasi) dan data yang dapat diubah (mutable data). Dua konsep penting dalam functional programming adalah **currying** dan **function composition**.

## Currying
**Currying** adalah teknik transformasi sebuah fungsi yang mengambil beberapa argumen menjadi serangkaian fungsi yang masing-masing mengambil satu argumen.

### Contoh
Misalkan kita memiliki fungsi untuk menjumlahkan 3 angka:

```js
function add(a,b,c){
  return a + b + c;
}
```

Fungsi tersebut bisa diubah menjadi curriedFunction seperti berikut.

```js
function curriedAdd(a) {
  return function(b) {
    return function (c) {
      return a + b + c;
    }
  }
}

// Menggunakan fungsi curried
const add5 = curriedAdd(2); // Mengikat nilai a = 2
const add5And3 = add5(3); // Mengikat nilai b = 3
const result = add5And3(10); // Menggunakan nilai c = 10

console.log(result); // Output: 15
console.log(curriedAdd(2)(3)(5)) // Output: 15
```

## Function Composition
**Composition** adalah teknik penggabungan beberapa fungsi menjadi satu fungsi yang menjalankan fungsi-fungsi tersebut secara berurutan dari kanan ke kiri.

### Penggunaannya

Misalnya kita memiliki beberapa fungsi sederhana:

```js
function add(x) {
  return x + 1;
}

function multiply(x) {
  return x * 2;
}
```

Kita bisa compose fungsi tersebut menjadi:

```js
const compose = (f, g) => (x) => f(g(x));

const addThenMultiply = compose(multiply, add);

console.log(addThenMultiply(5)); // Output: 12, karena (5 + 1) * 2 = 12
```

Kedua materi ini telah dijelaskan pada beweekly-beweekly sebelumnya, kita hanya mengulang kembali. Disini kita akan bahas bagaimana keduanya jika digabung.

### WHAT?
**Currying** dan **compotiotion** adalah konsep dasar dalam pemrograman fungsional yang sering digunakan bersama untuk menciptakan **fungsi kompleks** dari fungsi-fungsi sederhana. **Currying** mengubah fungsi dengan beberapa argumen menjadi serangkaian fungsi yang masing-masing menerima satu argumen. **Composition** menggabungkan beberapa fungsi sehingga keluaran dari satu fungsi menjadi masukan untuk fungsi berikutnya.

Menggunakan keduanya secara bersamaan memungkinkan pembuatan fungsi kompleks dengan cara yang bersih dan modular, meningkatkan keterbacaan dan pemeliharaan kode.

### Kapan ini digunakan?
Beberapa contoh penggunaannya meliputi: (kata si chatgpt)

- **Pemrosesan Data**: Membuat pipeline pemrosesan data dengan fungsi-fungsi kecil yang diterapkan secara berurutan.
- **Reusabilitas Kode**: Membuat fungsi yang dapat digunakan kembali di berbagai bagian aplikasi.
- **Pembuatan API**: Merancang API yang fleksibel dan modular.
- **Pengujian Unit**: Menulis tes yang lebih mudah dengan fungsi-fungsi kecil yang dapat diuji secara terpisah.

### Contoh

```js
// Fungsi curry
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn(...args);
        } else {
            return (...args2) => curried(...args, ...args2);
        }
    };
}

// Fungsi compose
function compose(...fns) {
    return function(result) {
        return fns.reduceRight((acc, fn) => fn(acc), result);
    };
}

// Contoh fungsi curried
const add = curry((a, b) => a + b);
const multiply = curry((a, b) => a * b);

// Menggunakan compose dengan fungsi curried
const add5AndMultiplyBy2 = compose(multiply(2), add(5));
console.log(add5AndMultiplyBy2(10)); // Output: 30
```

### LIVE CODE
Mari kita cobakan dengan menuliskannya pada [Replit](https://replit.com/@asruldev/frontend-sicepat#index.js)













