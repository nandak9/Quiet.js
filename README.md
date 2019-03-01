Quiet.js
===========

This is a javascript binding for [libquiet](https://github.com/quiet/quiet), a library for sending and receiving data via sound card. It can function either via speaker or cable (e.g., 3.5mm). Quiet comes included with a few transmissions profiles which configure quiet's transmitter and receiver. For speaker transmission, there is a profile which transmits around the 19kHz range, which is essentially imperceptible to people (nearly ultrasonic). For transmission via cable, quiet.js has profiles which offer speeds of at least 40 kbps.

Compatibility
--------
| Browser           | Transmitter             | Receiver                           |
| ------------------|-------------------------|------------------------------------|
| Chrome            | *Supported*             | *Supported*<sup>1</sup>            |
| Chrome (Android)  | *Supported*             | *Partially Supported*<sup>1,2</sup>|
| Edge              | *Supported*             | *Supported*                        |
| Firefox           | *Supported*             | *Partially Supported*<sup>3</sup>  |
| Firefox (Android) | *Supported*             | *Partially Supported*<sup>2,3</sup>|
| Internet Explorer | *Not Supported*         | *Not Supported*                    |
| Safari            | *Supported*             | *Not Supported*<sup>4</sup>        |
| Safari (iOS)      | *Supported*             | *Not Supported*<sup>4</sup>        |

[1]: For Chrome receivers, the page *must* be delivered via https. Chrome does not support microphone input without TLS.

[2]: GMSK profiles only

[3]: Firefox's WebAudio implementation resamples audio input to 32kHz, which limits all audio received to 16kHz and below. This means the ultrasonic profile cannot be used for Firefox receivers. Additionally, the resampler used by Firefox produces strong audio distortion, which makes reception by some profiles difficult. However, the audible profiles work well. For the most recent information on this limitation.

[4]: Safari does not support `getUserMedia` or microphone input in any capacity.

Usage
--------
Quiet-js includes a blob of libquiet compiled by emscripten as well as a javascript binding for ease of use. The bindings must be loaded before the compiled portion. Below is the recommended way to include Quiet in your project.

```
    <script type="text/javascript" src="quiet.js"></script>
    <script type="text/javascript" src="your_project.js"></script>
    <script async type="text/javascript" src="quiet-emscripten.js"></script>
```

Additionally, the emscripten compiled portion requires a memory initializer, `quiet-emscripten.js.mem`. This is loaded asynchronously by `quiet-emscripten.js`.

**It is strongly recommended to also include libfec.js. An emscripten-compiled version of libfec may be found [here](https://github.com/quiet/libfec/releases) or with `npm install libfec`.** If libfec is not included, then quiet.js will not be able to use any profiles which use convolutional codes or Reed-Solomon error correction.

For a complete example demonstrating ultrasonic text transmission and reception.


