Forked from [GitHub - caemor/epd-waveshare: Drivers for various EPDs from Waveshare](https://github.com/caemor/epd-waveshare) for SPI e-paper displays from Dalian Good Display.

It uses the [embedded graphics](https://crates.io/crates/embedded-graphics) library for the optional graphics support.

A 2018-edition compatible version (Rust 1.31+) is needed.

Other similar libraries with support for much more displays are [u8g2](https://github.com/olikraus/u8g2) and [GxEPD](https://github.com/ZinggJM/GxEPD) for Arduino.

## Examples

There are multiple examples in the examples folder. Use `cargo run --example epd3in71bw` to try them.

```Rust
// Setup the epd
let mut epd = EPD3in71bw::new(&mut spi, cs, busy, dc, rst, &mut delay)?;

// Setup the graphics
let mut display = Display3in71bw::default();

// Draw some text
display.draw(
    let _ = Text::new("Hello Rust!", Point::new(x, y))
        .into_styled(text_style!(
            font = Font12x16,
            text_color = Black,
            background_color = White
        ))
        .draw(display);
);

// Transfer the frame data to the epd and display it
epd.update_and_display_frame(&mut spi, &display.buffer())?;
```

## (Supported) Devices

| Device (with Link) | Colors | Flexible Display | Partial Refresh | Supported | Tested |
| :---: | --- | :---: | :---: | :---: | :---: |
| [3.71 Inch E-paper](http://www.e-paper-display.cn/products_detail/productId=411.html) | Black, White | ✕ | ✕ | ✔ | ✔ |
| [3.71 Inch E-paper](http://www.e-paper-display.com/products_detail/productId=462.html) | Black, White, Red | ✕ | ✕ | ✕ | ✕ |

### Interface

| Interface | Description |
| :---: |  :--- |
| VCC 	|   3.3V |
| GND   | 	GND |
| DIN   | 	SPI MOSI |
| CLK   | 	SPI SCK |
| CS    | 	SPI chip select (Low active) |
| DC    | 	Data/Command control pin (High for data, and low for command) |
| RST   | 	External reset pin (Low for reset) |
| BUSY  | 	Busy state output pin (Low for busy)  |
