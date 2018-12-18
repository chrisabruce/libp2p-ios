# libp2p iOS

Attempt to get [libp2p-rs](https://github.com/libp2p/rust-libp2p) working on iOS.

## Getting Started

This project is in "hacking" mode at the moment.  The goal is to get libp2p-rs to compile for iOS so can be used in an iOS application.

### Prerequisites

What things you need to install the software and how to install them

```
TODO
```

### Installing


Setup
-----

1. Install the common build tools like C compiler and linker. On macOS, get
    Xcode, and install the command line tools.

    ```sh
    xcode-select --install
    ```

2. Download [rustup](https://www.rustup.rs/). We will use this to setup Rust for
   cross-compiling.

    ```sh
    curl https://sh.rustup.rs -sSf | sh
    ```

3. Download targets for iOS

    ```sh
    # iOS. Note: you need *all* five targets
    rustup target add aarch64-apple-ios armv7-apple-ios armv7s-apple-ios x86_64-apple-ios i386-apple-ios

4. Install cargo-lipo to generate the iOS universal library.

    ```sh
    cargo install cargo-lipo
    ```


Creating the library
----------------------


1. Build the library.

    ```sh
    # iOS
    cargo lipo --release
    ```

2. Build the Xcode project. - TODO

    ```sh
    cd examples/ios
    xcodebuild -configuration Release -scheme RustChat | xcpretty
    cd ../..
    ```

    When you create an Xcode project yourself, note the following points:

    * Add the C header `rust_chat.h` to allow using the Rust functions from C.
    * Copy `target/universal/release/lib???.a` to the project. You may need
      to modify `LIBRARY_SEARCH_PATHS` to include the folder of the `*.a` file.
    * Note that `cargo-lipo` does not generate bitcode yet. You must set
      `ENABLE_BITCODE` to `NO`. (See also <http://stackoverflow.com/a/38488617>)
    * You need to link to `libresolv.tbd`.


## Contributing

Pull Requests welcome, but must be under the same license.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/chrisabruce/libp2p-ios/tags). 

## Authors

* **Chris Bruce** - *Initial work* - [Chris Bruce](https://github.com/chrisabruce)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

- [rust_ios_android](https://github.com/kennytm/rust-ios-android)