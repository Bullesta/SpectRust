# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2023-07-19
### Added
- Support for images with transparency (alpha channel). In the `locate_image` and `locate_center_on_screen` functions, pixels in the source image that are fully transparent are now ignored when comparing the image to the screenshot.
- Comments for code readability
  
### Changed
- Replaced Rgb use with Rgba

## [0.1.0] - 2023-07-17
Initial release

### Added
- Basic screen capture functionality
- Image location on the screen
- Support for regional capture
- Adjustable minimum confidence and tolerance parameters
