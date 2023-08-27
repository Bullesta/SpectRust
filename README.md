# SpectRust
<div align="left">
    <a href="https://i.ibb.co/FKvjWRF/spectrust-logo.png">
        <img class="logo" src="https://i.ibb.co/FKvjWRF/spectrust-logo.png" width="40%" height="40%">
    </a>
</div>

A Rust-based Computer visioner for locating images on screen

It can search the entire screen over 3x faster than pyautogui and does not require OpenCV for options like Confidence. I've also added an option called Tolerance that allows for leniency with pixel colors that are close to the original image's. Written in pure Rust.
```rust
locate_img_center(img: &DynamicImage, region: Option<(u16, u16, u16, u16)>, min_confidence: Option<f32>, tolerance: Option<u8>) -> Option<(u32, u32, f32)>)
```
```rust
locate_img(img: &DynamicImage, region: Option<(u16, u16, u16, u16)>, min_confidence: Option<f32>, tolerance: Option<u8>) 
```
**img**: required borrowed DynamicImage

**region**: requires tuple BoundingBox (x, y, width, height) (Default Entire Screen)

**min_confidence**: 0.1 - 1.0, percentage of how many of the pixels need to match (Default 0.95)

**tolerance**: 0 - 255, range of pixels to accept from image's pixels. So if an image has a pixel of 234, 52, 245 with a tolerance of 10, then the locator will accept values ranging from 224, 42, 235 - 244, 62, 255. (Default 5)


All of these requires (except img) are optional and require either a **Some()** or **None**

Examples:
```rust
use spectrust::*;
fn main () {
    let img = image::open("images.png").expect("Unable to locate file.");
    let region = None;
    let min_confidence = Some(0.8);
    let tolerance = Some(5);

    match locate_center_of_image(&img, region, min_confidence, tolerance) {
        Some((x, y, confidence)) => {
            println!("Image center found at {}, {} with confidence {}", x, y, confidence);
        },
        None => println!("Image not found"),
    }
}
```
```rust
fn main() {
    let img = image::open("images.png").expect("Unable to locate file.");

    match locate_image(&img, None, None, None) {
        Some((x, y, img_width, img_height, _confidence)) => {
            println!("x: {}, y: {}, width: {}, height: {}",x, y, img_width, img_height)
        },
        None => println!("Image not found")
    }
}
```
If you are having trouble with finding an image. Try lowering the confidence or increasing the tolerance or contact me through discord: bullesta

Benchmark
--------
**Python**: 150ms
**Rust**: 53ms
(Both finding the Rust icon with a size of 225x225px on a 1920x1080 screen)

**Useful for Bot Creating**
<div align="center">
    <div>
    <a href="https://s11.gifyu.com/images/SWCfO.gif">
        <img src="https://s11.gifyu.com/images/SWCfO.gif">
    </a>
    <div>
        *Reaction Test (actual time is about 12ms)
    </div>
    <div>
    <a href="https://i.ibb.co/5hndWVg/Clicker-Game-REsults.png">
      <img src="https://i.ibb.co/5hndWVg/Clicker-Game-REsults.png">
    </a>
    </div>
    <div>
        *Running for 20 minutes on an online aim trainer
    </div>
</div>
