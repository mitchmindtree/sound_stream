# DEPRECATED

[rust-portaudio](https://github.com/jeremyletang/rust-portaudio)'s API has improved enough to the point where **sound_stream** is no longer necessary.

# SoundStream [![Build Status](https://travis-ci.org/RustAudio/sound_stream.svg?branch=master)](https://travis-ci.org/RustAudio/sound_stream)

A simple-as-possible, *fast* audio I/O stream wrapping PortAudio for Rust! It looks like this:

```Rust
// The callback we'll use to pass to the Stream. It will write the input directly to the output.
let f = Box::new(move |input: &[f32], _: Settings,
                       output: &mut[f32], _: Settings,
                       dt: f64, _: CallbackFlags| {
    for (output_sample, input_sample) in o.iter_mut().zip(i.iter()) {
        *output_sample = *input_sample;
    }
    CallbackResult::Continue
});

// Run our callback on the default, duplex, non-blocking stream.
let stream = SoundStream::new()
    .duplex(StreamParams::new(), StreamParams::new())
    .run_callback(f)
    .unwrap();
```


Usage
-----

Add sound_stream to your Cargo.toml dependencies like so:

```
[dependencies]
sound_stream = "*"
```

For more details, see [the example](https://github.com/RustAudio/sound_stream/blob/master/examples/test.rs).

PortAudio
---------

SoundStream uses [PortAudio](http://www.portaudio.com) as a cross-platform audio backend. The [rust-portaudio](https://github.com/jeremyletang/rust-portaudio) dependency will first try to find an already installed version on your system before trying to download it and build PortAudio itself.

License
-------

MIT - Same license as [PortAudio](http://www.portaudio.com/license.html).

