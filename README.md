# ocaml-cordova-plugin-barcodescanner

[![LGPL-v3 licensed](https://img.shields.io/badge/license-LGPLv3-blue.svg)](https://raw.githubusercontent.com/dannywillems/ocaml-cordova-plugin-barcodescanner/master/LICENSE)
[![Build Status](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-barcodescanner.svg?branch=master)](https://travis-ci.org/dannywillems/ocaml-cordova-plugin-barcodescanner)

Binding to
[cordova-plugin-barcodescanner](https://github.com/apache/cordova-plugin-barcodescanner)

[Example
application](https://github.com/dannywillems/ocaml-cordova-plugin-barcodescanner-example).

## What does cordova-plugin-barcodescanner do ?

```
This plugin defines a global navigator.barcodescanner object, which provides an API for
taking pictures and for choosing images from the system's image library.
```

Source: [cordova-plugin-barcodescanner](https://github.com/apache/cordova-plugin-barcodescanner)

## Repository branches and tags

We are migrating bindings from
[js_of_ocaml](https://github.com/ocsigen/js_of_ocaml) (low level bindings) to
[gen_js_api](https://github.com/lexifi/gen_js_api) (high level bindings).

The gen_js_api binding allows to use *pure* ocaml types (you don't have to use
the ## syntax from js_of_ocaml or Js.string type but only # and string type).

The js_of_ocaml version is available in the branch
[*js_of_ocaml*](https://github.com/dannywillems/ocaml-cordova-plugin-barcodescanner/tree/js_of_ocaml)
but we **recommend** to use the gen_js_api version which is the master branch.

## How to install and compile your project by using this plugin ?

Don't forget to switch to a compiler **>= 4.03.0**.
```Shell
opam switch 4.03.0
```

You can use opam by pinning the repository with
```Shell
opam pin add cordova-plugin-barcode-scanner https://github.com/dannywillems/ocaml-cordova-plugin-barcodescanner.git
```

and to compile your project, use
```Shell
ocamlfind ocamlc -c -o [output_file] -package gen_js_api -package cordova-plugin-barcode-scanner [...] -linkpkg [other arguments]
```

Don't forget to install the cordova plugin barcodescanner with
```Shell
phonegap plugin add phonegap-plugin-barcodescanner
```

## How to use ?

See the official documentation
[cordova-plugin-barcodescanner](https://github.com/phonegap/phonegap-plugin-barcodescanner)

## ! BE CAREFUL !

The plugin creates a new object called *barcodeScanner*, but the object is
available when the *deviceready* event is handled.

We provide a function *Cordova_barcode_scanner.t* of type *unit -> Cordova_barcode_scanner.barcode_scanner* which creates the
binding to the *barcodeScanner* js object. You must call it when the deviceready
event is handled.
By using the [binding to the cordova
object](https://github.com/dannywillems/ocaml-cordova), you need to use

```OCaml
let on_device_ready () =
  let b = Cordova_barcode_scanner.t () in
  (* Some code *)

let _ = Cordova.Event.device_ready on_device_ready
